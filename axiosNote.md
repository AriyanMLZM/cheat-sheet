## Create Axios Instance

```
export default axios.create({
  baseURL: 'BASE_URL',
  headers: {
    'Content-Type': 'application/json',
    'Accept': 'application/json'
  }
});
```

we can create an instance with config and use it for our requests in faster way.  
we can overwrite the config when using the instance.

`const res = await axiosInstance[method](url, requestConfig)`

we can use the cruds on instance.

`const response = await axiosInstance.get("/path")`  
`await axiosInstance.post("/path", data)`
