<!-- src/views/releasenote/FF14.vue -->
<template>
  <div>
    <CTable striped :columns="column" :items="groupList" />
  </div>
</template>

<script>
import axios from 'axios';
import FF14 from '@/views/releasenote/ff14.json';

const groupList = FF14;

export default {
  data() {
    return {
      column: [
        {
          key: 'category',
          label: 'Category',
          _props: { scope: 'col' },
        },
        {
          key: 'text',
          label: 'Text',
          _props: { scope: 'col' },
        },
        {
          key: 'date',
          label: 'Date',
          _props: { scope: 'col' },
        },
      ],
      groupList,
    };
  },
};
</script>
