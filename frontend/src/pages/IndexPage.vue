item>
            <q-item-section>
              <q-item-label>Advanced Git</q-item-label>
              <q-item-label caption>{{ apiData.git.detail }}</q-item-label>
            </q-item-section>
          </q-item>
          <q-item>
            <q-item-section>
              <q-item-label>Advanced Docker</q-item-label>
              <q-item-label caption>{{ apiData.docker.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
        <q-btn v-if="!loading" color="primary" @click="fetchData">Refresh Data</q-btn>
      </q-card-section>
    </q-card>
  </q-page>
</template>


<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';


// จากตัวอย่างก่อน
const gitSteps = [ /* ... (same as before) */ ];
const dockerItems = [ /* ... (same as before) */ ];


const apiData = ref({ git: {}, docker: {} });
const loading = ref(true);


const fetchData = async () => {
  loading.value = true;
  try {
    const response = await axios.get(import.meta.env.VITE_API_URL + '/api/demo');
    apiData.value = response.data;
  } catch (error) {
    console.error('API Error:', error);
  } finally {
    loading.value = false;
  }
};


onMounted(fetchData);
</script>
