<script lang="ts" setup>
  import { ref, computed, onMounted } from 'vue'
  import type { Ref } from 'vue'
  import ListItem from './ListItem.vue'

  type Item = {
    title: string
    checked?: boolean
  }
  //  Ref is used to type the value and lowercase ref is used as a wrapper of the array of items
  const listItems: Ref<Item[]> = ref([
    {
      title: 'Make a todo list app',
      checked: true
    },
    {
      title: 'Predict The Weather App',
      checked: true
    },
    {
      title: 'Play some tunes',
      checked: true
    },
    {
      title: 'Let\'s get cooking',
      checked: true
    },
    {
      title: 'Organize a game night',
      checked: false
    },
    {
      title: 'Publish my work',
      checked: true,
    },
    {
      title: 'Learn a new language',
      checked: false
    },
    {
      title: 'Pump some iron',
      checked: true
    },
    {
      title: 'Track my expenses',
      checked: false
    }
  ])

  const updateItem = (item: Item): void => {
    const updatedItem = findItemInList(item)
    if (updatedItem) {
      toggleItemStatus(updatedItem)
      setToStorage(storageItem.value)
    }
  }

  const findItemInList = (item: Item) => {
    return storageItem.value.find((itemInList: Item) => itemInList.title === item.title)
  }

  const toggleItemStatus = (item: Item): void => {
    item.checked =!item.checked
  }

  // Sorting List Items

  const sortList = computed(() => [
   ...storageItem.value
  ].sort((a, b) => (a.checked? 1 : 0)) as unknown as Item[])

  // Preserving changes to the list
  const setToStorage = (items: Item[]): void => {
    localStorage.setItem('item-items', JSON.stringify(items))
  }

  const getFromStorage = (): Item[] | [] => {
    const stored = localStorage.getItem('list-items')
    if (stored) {
      return JSON.parse(stored)
    }
    return []
  }

  // list to be retrieved in the browser, We can use onMounted hook to retrieve the data from the storage
  // Reactive variable to hold the items
  const storageItem: Ref<Item[]> = ref([])

  // Item not exist it will mounted back with the default items
  const initListItems = (): void => {
    if (storageItem.value.length === 0) {
      const listItems = [
        { title: 'Make a todo list app', checked: true },
        { title: 'Predict the weather', checked: false },
        { title: 'Read some comics', checked: false },
        { title: 'Let\'s get cooking', checked: false },
        { title: 'Pump some iron', checked: false },
        { title: 'Track my expenses', checked: false },
        { title: 'Organise a game night', checked: false },
        { title: 'Learn a new language', checked: false },
        { title: 'Publish my work' }
      ]
      setToStorage(listItems)
      storageItem.value = listItems
    }
  }

  onMounted(() => {
    initListItems()
    storageItem.value = getFromStorage()
  })

</script>


<template>
  <ul>
    <!-- v-for is directive loop over the '<li>' every item are assigned to first argument 'item' and the index for 'key' key attribute help keep track of the changes that are being made so that it can update the DOM more effectively -->
    <li :key='key' v-for='(item, key) in listItems'>
      <!-- v-on is to  bind event listener -->
      <!--.prevent modifier to prevent the default behavior of the checkbox mechanics -->
      <ListItem :is-checked='item.checked' v-on:click="updateItem(item)">{{ item.title }}</ListItem>
    </li>
  </ul>
</template>

<style scoped>
ul {
  list-style-type: none;
  padding: 5rem;
  height: 100vh;
  width: auto;
}

li {
  margin: 0.4rem 0;
}
</style>