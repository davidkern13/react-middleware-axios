# react-middleware-axios

```
import { CALL_API_DATA, GET_API_DATA } from '../../store/contact-list/action-types';
import { API_URL } from '../../enum';
import { AxiosRequest } from '../../request';

const apiMiddleware =  (store) =>  (next) =>  (action) => {
     next(action);

     if(action.type === CALL_API_DATA){
        const { suffix = '', method = 'get' } = action.payload;

        AxiosRequest({method: method, url: API_URL + suffix, status: 400 }).then(res => {
            store.dispatch({ type: GET_API_DATA, payload: res })
        });
     }
}

export default apiMiddleware;
```
