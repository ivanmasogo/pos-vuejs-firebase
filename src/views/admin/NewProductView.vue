<script setup>
import { reactive } from 'vue'
import { useRouter } from 'vue-router'
import Link from '@/components/Link.vue'
import useImage from '@/composables/useImage'
import { useProductsStore } from '@/stores/products'

const { url, onFileChange, isImageUploaded } = useImage()
const products = useProductsStore()
const router = useRouter()

const formData = reactive({
  name: '',
  category: '',
  price: '',
  availability: '',
  image: ''
})

const submitHandler = async data => {
  const { image, ...values } = data

  try{
    await products.createProduct({
      ...values,
      image: url.value
    })

    router.push({name: 'products'})
  }catch(error){
    console.log(error)
  }
}
</script>

<template lang="pug">
div
  Link(to="products") Volver 
  h1(class="text-4xl font-black my-10") Nuevo Producto
  div(class="flex justify-center bg-white shadow")
    div(class="mt-10 p-10 w-full 2xl:w-2/4")
      FormKit(
        type="form"
        submit-label="Agregar Producto"
        incomplete-message="No se pudo enviar"
        @submit="submitHandler"
        :value="formData"
      )
        FormKit(
          type="text"
          label="Nombre"
          name="name"  
          placeholder="Nombre de Producto"
          validation="required"
          :validation-messages="{required : 'El nombre del producto es obligatorio'}"
          v-model.trim="formData.name"
        )
        FormKit(
          type="file"
          label="Imagen Producto"
          name="image"  
          placeholder="Nombre de Producto"
          validation="required"
          :validation-messages="{required : 'La imagen del producto es obligatoria'}"
          accept=".jpg"
          @change="onFileChange"
          v-model.trim="formData.image"

        )

        div(v-if="isImageUploaded")
          p(class="font-black") Imagen Producto:
          img(
            :src="isImageUploaded"
            alt="Nueva imagen producto"
            class="w-32"
          )
        FormKit(
          type="select"
          label="Categoría"
          name="category"  
          validation="required"
          :validation-messages="{required : 'La categoría es obligatoria'}"
          :options="products.categoryOptions"
          v-model.number="formData.category"

        )
        FormKit(
          type="number"
          label="Precio"
          name="price"  
          placeholder="Precio de Producto"
          validation="required"
          :validation-messages="{required : 'El precio es obligatorio'}"
          min="1"
          v-model.number="formData.price"

        )        
        FormKit(
          type="number"
          label="Disponibles"
          name="availability"  
          placeholder="Cantidad disponible"
          validation="required"
          :validation-messages="{required : 'La cantidad es obligatoria'}"
          min="1"
          v-model.trim="formData.availability"
        )    
</template>
