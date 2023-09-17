<template>
    <div>
      <!-- 1. Template Syntax -->
      <section>
        <!-- a. Text Interpolation -->
        <h1>{{ greeting }}</h1>

        <!-- b. Raw HTML [v-html] -->
        <p v-html="rawHTML"></p>

        <!-- c. Attribute Bindings [v-bind:id] -->
        <div :id="dynamicId">{{ dynamicText }}</div>

        <!-- d. JavaScript expressions inside syntax i.e.{{ }} -->
        <p>{{ 2 + 8 }}</p>
      </section>
  
      <!-- 2. Methods -->
      <section>
        <button @click="sayHello">Click me to say a message</button>
      </section>
  
      <!-- 3. Reactivity Fundamentals [ref(), <script setup>] -->
      <section>
        <p>{{ count }}</p>
        <button @click="incrementCount">+ Count</button>
      </section>
  
      <!-- 4. Computed Properties -->
      <section>
        <p>Computed Property: {{ computedValue }}</p>
      </section>
  
      <!-- 5. Class and Style Bindings -->
      <section>
        <!-- a. Binding HTML class [v-bind:class] -->
        <div :class="getClassObject">Styled Div</div>
        <!-- b. Binding Inline Styles [v-bind:style] -->
        <div :style="getStyleObject">Styled Div</div>
      </section>
  
      <!-- 6. List Rendering -->
      <section>
        <!-- a. v-for with an Object -->
        <ul>
          <li v-for="(item, key) in items" :key="key">{{ item }}</li>
        </ul>

        <!-- e. v-for with a Component -->
        <ul>
          <my-component
            v-for="(item, index) in items"
            :key="index"
            :item="item"
            @custom-event="handleCustomEvent"
          ></my-component>
        </ul>
      </section>
  
      <!-- 7. Event Handling: Listening to Events [v-on:click] -->
      <section>
        <!-- a. Inline Handlers -->
        <button @click="handleButtonClick">Button</button>
      </section>
  
      <!-- 8. Form Input Bindings -->
      <section>
        <!-- a. v-model with <input type="text">, <input type="checkbox">, <input type="radio">, <select> and <textarea> -->
        <input v-model="textInput" type="text" />
        <input v-model.lazy="lazyText" type="text" />
        <input v-model.number="numberInput" type="number" />
        <input v-model.trim="trimmedText" type="text" />
      </section>
  
      <!-- 9. Watchers -->
      <section>
        <p>Watched Value: {{ watchedValue }}</p>
      </section>
  
      <!-- 10. Components -->
      <section>
        <!-- a. Props -->
        <my-component :prop-value="componentProp" @custom-event="handleCustomEvent">
          <template #default>Slot Content</template>
        </my-component>
      </section>
  
      <!-- 11. Router -->
      <section>
        <router-link :to="{ name: 'home' }">Home</router-link>
        <router-link :to="{ name: 'about' }">About</router-link>
        <router-view></router-view>
      </section>
    </div>
  </template>
  
  <script>
  import { ref, computed, watch } from 'vue';
  
  export default {
    data() {
      return {
        greeting: 'Hello, Vue!',
        rawHTML: '<strong>Raw HTML</strong>',
        dynamicId: 'unique-id',
        dynamicText: 'Dynamic Text',
        count: ref(0),
        textInput: '',
        lazyText: '',
        numberInput: null,
        trimmedText: '',
        watchedValue: 'Initial Value',
        componentProp: 'Component Prop Value',
        items: ['Car 1', 'Car 2', 'Car 3', 'Orange', 'Apple'],
      };
    },
    computed: {
      computedValue() {
        return `Computed: ${this.count}`;
      },
      getClassObject() {
        return {
          active: this.count % 2 === 0,
          'text-danger': this.count % 2 !== 0,
        };
      },
      getStyleObject() {
        return {
          color: this.count % 2 === 0 ? 'green' : 'red',
          fontSize: '20px',
        };
      },
      filteredItems() {
        return this.items.filter(item => item.length > 3);
      },
    },
    methods: {
      sayHello() {
        alert('Hello!');
      },
      incrementCount() {
        this.count++;
      },
      handleButtonClick() {
        alert('Button Clicked');
      },
      handleCustomEvent(data) {
        alert(`Custom Event Fired with Data: ${data}`);
      },
    },
    watch: {
      watchedValue(newValue, oldValue) {
        console.log(`Value changed from ${oldValue} to ${newValue}`);
      },
    },
  };
  </script>
  
  <style scoped>
  .active {
    font-weight: bold;
  }
  .text-danger {
    color: red;
  }
  </style>
  