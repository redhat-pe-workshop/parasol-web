# Parasol Web Application

This is the source code for the Parasol Web application for the consumer insurance ecommerce portal.

# Technical details

This is written using Angular with Server-side rendering.  

## Dependencies

This is a single-page application (SPA), and is dependent on the `parasol-store` service for 

* Get paginated products list
* Product list
* Get customer details for logged in user
* Place order

# Running in local env

Run `npm run dev:ssr` for running this as server side app. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

To run the parasol-store and parasol-db images locally and setup these environment variables. These are part of the ConfigMap when deployed on OpenShit

```bash
export API_GET_PAGINATED_PRODUCTS="https://<host:port>/services/catalog/product"
export API_GET_PRODUCT_DETAILS_BY_IDS="http://<host:port>/services/catalog/product/:ids" 
export API_CART_SERVICE="http://<host:port>/services/cart"
export API_CUSTOMER_SERVICE="http://<host:port>/services/customer/id/:custId"
export API_ORDER_SERVICE="http://<host:port>/services/order"
```

User login is handled via Keycloak auth. You will also need to setup Keycloak, create a new client `parasol-web-gateway` on Keycloak. 
Setup following env variables to be able to perform auth and also setup Logout URI as shown below

```bash
export SSO_CUSTOM_CONFIG="parasol-web-gateway"
export SSO_AUTHORITY="http://<host:port>>/realms/<realm-name>"
export SSO_REDIRECT_LOGOUT_URI="http://<host:port>>/home"
export SSO_LOG_LEVEL=2
```



# Build & Push a Container Image

```bash
podman build -t quay.io/redhat_pe_workshop/parasol-web:<tag> .

podman push quay.io/redhat_pe_workshop/parasol-web:<tag> 
```
