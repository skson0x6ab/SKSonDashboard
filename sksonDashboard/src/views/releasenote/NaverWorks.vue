<!-- src/views/releasenote/NaverWorks.vue -->
<template>
  <div>
    <CTable striped :columns="column" :items="groupList" />
  </div>
</template>

<script>
import naverJson from '@/views/releasenote/naverworks.json';

const groupList = naverJson;

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
