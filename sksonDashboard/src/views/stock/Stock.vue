<!-- src/views/stock/Stock.vue -->
<template>
  <div>
    <CTable bordered striped :columns="column" :items="jsonData">
    </CTable>
  </div>
</template>

<script>
import githubApi from '@/services/githubApi';

export default {
  data() {
    return {
      jsonData: null,
    };
  },
  methods: {
    async fetchJsonData() {
      try {
        // 레포지토리 소유자와 이름, 파일 경로를 설정합니다.
        const owner = 'skson0x6ab';
        const repo = 'DataRepository';
        const filePath = 'PublicOfferingStockSchedule.json';

        // GitHub API를 통해 파일의 내용을 가져옵니다.
        const response = await githubApi.get(
          `/repos/${owner}/${repo}/contents/${filePath}`
        );

        // Base64 문자열을 UTF-8로 디코딩
        const base64Content = response.data.content;
        const binaryString = atob(base64Content);
        const binaryLength = binaryString.length;
        const bytes = new Uint8Array(binaryLength);

        for (let i = 0; i < binaryLength; i++) {
          bytes[i] = binaryString.charCodeAt(i);
        }

        const textDecoder = new TextDecoder('utf-8');
        const decodedContent = textDecoder.decode(bytes);

        // JSON으로 파싱
        this.jsonData = JSON.parse(decodedContent);
      } catch (error) {
        console.error('데이터를 가져오는 중 오류가 발생했습니다:', error);
      }
    },
  },
  created() {
    this.fetchJsonData();
  },
};
</script>
