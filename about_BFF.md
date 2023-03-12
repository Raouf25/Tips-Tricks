# Many environments and many API's to call in my Back For Front ?


## Configuration
La classe "API.ts"
```ts
import axios, { AxiosInstance, AxiosRequestConfig, AxiosResponse } from 'axios'

const BASE_URL = 'http://localhost:8082'

class AxiosService {
  private instance: AxiosInstance;

  constructor (baseURL: string) {
    this.instance = axios.create({
      baseURL,
      timeout: 30000,
      headers: {
        'Content-Type': 'application/json'
      }
    })

    this.instance.interceptors.request.use(
      (config) => {
        config.url = config.url?.split('|').join('%7C')
        return config
      },
      (error) => {
        return Promise.reject(error)
      }
    )

    this.instance.interceptors.response.use(
      (response: AxiosResponse) => {
        return response
      },
      (error) => {
        return Promise.reject(error)
      }
    )
  }

  get<T> (url: string): Promise<AxiosResponse<T>> {
    return this.instance.get<T>(url)
  }

  post<T> (url: string, data: any, config?: AxiosRequestConfig): Promise<AxiosResponse<T>> {
    return this.instance.post<T>(url, data, config)
  }

  put<T> (url: string, data: any, config?: AxiosRequestConfig): Promise<AxiosResponse<T>> {
    return this.instance.put<T>(url, data, config)
  }

  delete<T> (url: string, config?: AxiosRequestConfig): Promise<AxiosResponse<T>> {
    return this.instance.delete<T>(url, config)
  }
}

const axiosService = new AxiosService(BASE_URL)
export default axiosService

```
## Definition des services 
Comment utiliser cette classe de configuration pour Appeler les différentes Servics 
exemple service-1.ts

```ts 
import Api from '@/services/Api'
import Country from ''@/services/dtos/Country'

export default {
 
  async getCountries (): Promise<Country[]> {
   // get(`http://localhost:8082/countries`);
    const response = await Api.get<Country[]>('/countries')
    return response.data
  },
 ....
}
```

## Utilisation de service
Utilisation de service dans un composant vue par exemple :
```ts 
<script lang="ts">
import { Vue } from 'vue-property-decorator'
import Country from '@/services/dtos/Country'
import service-1 from '@/services/service-1'


export default class TopNavbar extends Vue {

  private countries: string[] = [];

private async getALLCountries () {
    const countrieDtos: Country[] = await service-1.getCountries()
   ....
  }
  ...
}
</script>
```
