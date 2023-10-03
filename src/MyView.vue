<template>
  <div>
    <!-- 1. Template Syntax -->
    <!-- a. Text Interpolation -->
    <h1>{{ message }}</h1>

    <!-- b. Raw HTML [v-html] -->
    <div v-html="rawHTML"></div>

    <!-- c. Attribute Bindings [v-bind:id] -->
    <div :id="elementId">{{ dynamicAttribute }}</div>

    <!-- d. JavaScript expressions inside syntax i.e.{{ }} -->
    <p>{{ a + b }}</p>

    <!-- ... -->

    <!-- 5. Class and Style Bindings -->
    <!-- a. Binding HTML class [v-bind:class] -->
    <div :class="{ 'active': isActive, 'error': hasError }">Class and Style Bindings</div>

    <!-- b. Binding Inline Styles [v-bind:style] -->
    <div :style="{ color: textColor }">Class and Style Bindings</div>

    <!-- ... -->

    <!-- 6. List Rendering -->
    <!-- a. v-for with an Object -->
    <ul>
      <li v-for="(item, key) in objectList" :key="key">{{ key }}: {{ item }}</li>

      <!-- b. v-for with a Range -->
      <li v-for="n in 5" :key="n">Item {{ n }}</li>

      <!-- c. v-for on <template> -->
      <template v-for="(item, index) in items" :key="index">
        <li>{{ item }}</li>
      </template>

      <!-- d. v-for with v-if -->
      <li v-for="(item, key) in filteredItems" :key="key">{{ item }}</li>

      <!-- e. v-for with a Component -->
      <child-component v-for="(component, index) in components" :key="index" :name="component.name"></child-component>
    </ul>

    <!-- ... -->

    <!-- 7. Event Handling -->
    <!-- a. Inline Handlers -->
    <button @click="sayHello">Say Hello</button>
    <button @click="inlineHandler">Inline Handler</button>
    <button @click="methodHandler">Method Handler</button>

    <!-- ... -->

    <!-- 8. Form Input Bindings -->
    <!-- a. v-model with <input type="text">, <input type="checkbox">, <input type="radio">, <select> and <textarea> -->
    <input type="text" v-model="textModel" />
    <input type="checkbox" v-model="checkboxModel" />
    <input type="radio" v-model="radioModel" :value="radioOption1" />
    <select v-model="selectedOption">
      <option value="option1">Option 1</option>
      <option value="option2">Option 2</option>
    </select>
    <textarea v-model="textareaModel"></textarea>

    <!-- b. v-model modifiers [.lazy , .number, .trim] -->
    <input type="text" v-model.trim="textModel" />
    <input type="checkbox" v-model.number="checkboxModel" />
    <input type="radio" v-model.trim="radioModel" :value="radioOption1" />
    <textarea v-model.lazy="textareaModel"></textarea>

    <!-- ... -->

    <!-- 9. Watchers -->
    <p>Reactive Value: {{ reactiveValue }}</p>

    <!-- 10. Components -->
    <!-- a. Props -->
    <child-component :name="computedValue" @custom-event="handleCustomEvent"></child-component>

    <!-- b. Events [$emit] -->
    <child-component @custom-event="handleCustomEvent"></child-component>

    <!-- c. Slots -->
    <child-component>
      <template v-slot:default>Slot Content</template>
    </child-component>

    <!-- 11. Router -->
    <!-- Navigation Links -->
    <router-link to="/about">About</router-link>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue';
import ChildComponent from './components/ChildComponent.vue';

// 1. Template Syntax
const message = ref('Hello, Vue!');
const rawHTML = '<span style="color: red;">Red Text</span>';
const elementId = 'unique-id';

// 3. Reactivity Fundamentals
const reactiveValue = ref(0);

// 4. Computed Properties
const a = 2;
const b = 3;
const computedValue = computed(() => a + b);

// 5. Class and Style Bindings
const isActive = ref(true);
const hasError = ref(false);
const textColor = 'blue';

// 6. List Rendering
const objectList = { a: 'Apple', b: 'Banana', c: 'Cherry' };
const items = [1, 2, 3, 4, 5];
const components = [{ id: 1, name: 'Component A' }, { id: 2, name: 'Component B' }];
const shouldShow = (item) => item > 2;

// 8. Form Input Bindings
const textModel = ref('');
const checkboxModel = ref(false);
const radioModel = ref('option1');
const selectedOption = ref('option1');
const textareaModel = ref('');

// 9. Watchers
watch(textModel, (newValue, oldValue) => {
    console.log('Text Model Watcher:', newValue, oldValue);
});

// 7. Event Handling
const sayHello = () => {
    alert('Hello!');
};
const inlineHandler = () => {
    alert('Inline Handler');
};
const methodHandler = () => {
    alert('Method Handler');
};

// 10. Components
const handleCustomEvent = (data) => {
    console.log('Custom event received:', data);
};
</script>
