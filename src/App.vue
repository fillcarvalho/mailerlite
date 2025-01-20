<template>
  <div class="container mx-auto my-3">
    <div class="col-1">
      <button class="btn btn-secondary button" @click="add('image')">
        Add Image
      </button>
      <button class="btn btn-secondary button" @click="add('text')">
        Add Text
      </button>
    </div>

    <div class="col-7">
      <h3>Draggable</h3>
      <draggable
        tag="div"
        :list="list"
        class="list-group"
        item-key="index"
        :animation="200"
      >
        <template #item="{ element, index }">
          <div class="py-2">
            <div>
              <component
                :is="element.type"
                class="list-group-item bg-gray-300 m-1 p-3 rounded-md cursor-pointer"
                :key="index"
                v-bind="element.props"
                @content-update="contentUpdate"
                :id="element.id"
                :current-image-id="element.props.imageId"
              />
              <i class="fa fa-times close" @click="removeAt(index)"></i>
              <i class="fa-solid fa-clone" @click="duplicate(index)"></i>
            </div>
          </div>
        </template>
      </draggable>
    </div>
    <div>
      <pre>{{ getJson() }}</pre>
    </div>
  </div>
</template>

<script>
var id = 0;
import { ref } from "vue";
import draggable from "vuedraggable";
import ContentImage from "./components/ContentImage.vue";
import ContentText from "./components/ContentText.vue";

const BLOCK_DEFAULT_PROPS = {
  imageUrl: null,
  imageId: 0,
  text: "",
};

const DEFAULT_IMAGE_ELEMENT = {
  id: 0,
  type: "ContentImage",
  props: { ...BLOCK_DEFAULT_PROPS },
};
const DEFAULT_TEXT_ELEMENT = {
  id: 0,
  type: "ContentText",
  props: { ...BLOCK_DEFAULT_PROPS },
};

export default {
  components: {
    draggable,
    ContentImage,
    ContentText,
  },
  setup() {
    const list = ref([]);

    
    /**
     * Removes the element at a specific position on the array
     * 
     * @param idx number
     */
    const removeAt = (idx) => {
      list.value.splice(idx, 1);
    };

    /**
     * Duplicates the content element
     * 
     * @param idx number
     */
    const duplicate = (idx) => {
      const elementToClone = list.value.find((el, index) => index === idx);

      if (elementToClone) {
        id++;
        const newElement = {
          ...elementToClone,
          props: { ...elementToClone.props },
        };
        newElement.id = id;
        list.value.splice(idx, 0, newElement);
      }
    };

    /**
     * Adds an element in the content element list
     * @param type string
     */
    const add = (type) => {
      let obj;
      switch (type) {
        case "image":
          obj = DEFAULT_IMAGE_ELEMENT;
          break;
        case "text":
          obj = DEFAULT_TEXT_ELEMENT;
          break;
      }

      id++;
      const newElement = { ...obj, props: { ...obj.props } };
      newElement.id = id;
      newElement.name = "Juan " + id;
      list.value.push(newElement);
    };

    /**
     * Returning the json with all the component information
     */
    const getJson = () => {
      return list.value;
    };

    /**
     * Receives the new values and update it at the object
     * @param value Object
     */
    const contentUpdate = (value) => {
      if (!value.id) {
        return;
      }
      const item = getItemById(value.id);

      if (item.length > 0) {
        if (item[0].type === "ContentText") {
          item[0].props.text = value.html;
        } else if (item[0].type === "ContentImage") {
          item[0].props.imageUrl = value.url;
          item[0].props.imageId = value.imageId;
        } else {
          throw new TypeError("Unhandled content type", filename)
        }
      }
    };

    /**
     * Returns an element from the content element list by Id
     * @param idx 
     */
    const getItemById = (idx) => {
      return list.value.filter((e) => e.id == idx);
    };

    return {
      removeAt,
      duplicate,
      add,
      getJson,
      list,
      contentUpdate,
    };
  },
};
</script>
<style scoped>

</style>