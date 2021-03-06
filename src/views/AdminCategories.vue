<template>
  <div class="container py-5">
    <AdminNav />

    <form class="my-4">
      <div class="form-row">
        <div class="col-auto">
          <input
            type="text"
            v-model="newCategoryName"
            class="form-control"
            placeholder="新增餐廳類別..."
          >
        </div>
        <div class="col-auto">
          <button
            type="button"
            class="btn btn-primary"
            @click.stop.prevent="createCategory(newCategoryName)"
          >
            新增
          </button>
        </div>
      </div>
    </form>
    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th
            scope="col"
            width="60"
          >
            #
          </th>
          <th scope="col">
            Category Name
          </th>
          <th
            scope="col"
            width="210"
          >
            Action
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="category in categories"
          :key="category.id"
        >
          <th scope="row">
            {{ category.id }}
          </th>
          <td class="position-relative">
            <div 
              v-show="!category.isEditing"
              class="category-name"
            >
              {{ category.name }}
            </div>
            <input
              v-show="category.isEditing"
              v-model="category.name"
              type="text"
              class="form-control"
            >
            <span
              v-show="category.isEditing"
              class="cancel"
              @click="handleCancel(category.id)"
            >
              ✕
            </span>
          </td>
          <td class="d-flex justify-content-between">
            <button
              v-show="!category.isEditing"
              type="button"
              class="btn btn-link mr-2"
              @click.stop.prevent="toggleIsEditing(category.id)"
            >
              Edit
            </button>
            <button
              v-show="category.isEditing"
              type="button"
              class="btn btn-link mr-2"
              @click.stop.prevent="updateCategory({ categoryId: category.id, name: category.name })"
            >
              Save
            </button>
            <button
              type="button"
              class="btn btn-link mr-2"
              @click.stop.prevent="deleteCategory(category.id)"
            >
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import AdminNav from '@/components/AdminNav'
import adminAPI from '../apis/admin'
import { Toast } from './../utils/helpers'

export default {
  components: {
    AdminNav
  },
  data () {
    return {
      categories: [],
      newCategoryName: ''
    }
  },
  created () {
    this.fetchCategories()
  },
  methods: {
    async fetchCategories () {
      try {
        const { data, statusText } = await adminAPI.categories.get()

        if (statusText !== 'OK') {
          throw new Error(statusText)
        }

        this.categories = data.categories.map((category) => ({
          ...category,
          isEditing: false
        }))
      } catch(err) {
        Toast.fire({
          type: 'error',
          title: 'something wrong..., '
        })
      }      
    },
    async createCategory (name) {
      try {
        const { data, statusText } = await adminAPI.categories.create({ name })

        if ((data.status !== 'success') || (statusText !== 'OK')) {
          throw new Error(statusText)
        }

        this.categories.push({
          id: data.categoryId,
          name: this.newCategoryName
        })

        this.newCategoryName = '' //clear the input field
      } catch (err) {
        Toast.fire({
          type: 'error',
          title: 'something wrong..., unable to create'
        })
      }
    },
    async deleteCategory (categoryId) {
      try {
        const { data, statusText } = await adminAPI.categories.delete({ categoryId })

        if ((data.status !== 'success') || (statusText !== 'OK')) {
          throw new Error(statusText)
        }

        this.categories = this.categories.filter(
          (category) => category.id !== categoryId
        )
      } catch (err) {
        Toast.fire({
          type: 'error',
          title: 'something wrong..., unable to delete'
        })
      }
      
    },
    toggleIsEditing (categoryId) {
      this.categories = this.categories.map(category => {
        if (category.id !== categoryId) return category
        // 如果迴圈中的 category.id 是欲修改的 categoryId 則改變 isEditing 的值
        return {
          ...category,
          nameCached: category.name,
          isEditing: !category.isEditing
        }
      })
    },
    async updateCategory ({ categoryId, name }) {
      try {
        this.toggleIsEditing(categoryId)
        const { data, statusText } = await adminAPI.categories.update({
          categoryId,
          name
        })
        
        if ((data.status !== 'success') || (statusText !== 'OK')) {
          throw new Error(statusText)
        }
      } catch (err) {
        Toast.fire({
          type: 'error',
          title: 'something wrong..., unable to update'
        })
      }
    },
    handleCancel (categoryId) {
      this.categories = this.categories.map(category => {
        if (category.id !== categoryId) return category

        return {
          ...category,
          name: category.nameCached,
        }
      })
      this.toggleIsEditing(categoryId)
    }
  }
}
</script>

<style scoped>
.category-name {
  padding: 0.375rem 0.75rem;
  border: 1px solid transparent;
  outline: 0;
  cursor: auto;
}

.btn-link {
  width: 62px;
}

.cancel {
  position: absolute;
  right: 20px;
  top: 50%;
  transform: translateY(-50%);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 25px;
  height: 25px;
  border: 1px solid #aaaaaa;
  border-radius: 50%;
  user-select: none;
  cursor: pointer;
  font-size: 12px;
}
</style>
