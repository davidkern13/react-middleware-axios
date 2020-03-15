# react-middleware-axios

### middleware
```
import { CALL_API_DATA, GET_API_DATA } from '../../store/contact-list/action-types';
import { API_URL } from '../../enum';
import { AxiosRequest } from '../../request';

const apiMiddleware =  (store) =>  (next) =>  (action) => {
     next(action);

     if(action.type === CALL_API_DATA){
        const { suffix = '', method = 'get' } = action.payload;

        AxiosRequest({method: method, url: API_URL + suffix }).then(res => {
            store.dispatch({ type: GET_API_DATA, payload: res })
        });
     }
}

export default apiMiddleware;
```


### action-types
```
export const CALL_API_DATA = 'CALL_API_DATA';
export const GET_API_DATA = 'GET_API_DATA';
export const ERROR_API_DATA = 'ERROR_API_DATA';
```

### API_URL
```
export const API_URL = '___URL___';
```

### AxiosRequest
```
import axios from 'axios';

export const AxiosRequest = (request) => {
      const data = axios(request).then( res => {
          return res.data;
      }).catch(error => {
          return error;
      });
      return data;
}
```

### action
```
import * as types from './action-types';

export const callApi = () => {
    return {
        type: types.CALL_API_DATA,
        payload: {
            suffix: 'contact_list',
            method: 'get'
        }
     }
};
```
