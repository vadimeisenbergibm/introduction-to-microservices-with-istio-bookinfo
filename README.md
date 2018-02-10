# istio-tutorial
tutorial for istio.io, based on [Istio Bookinfo Sample](https://istio.io/docs/guides/bookinfo.html).

1. Download Istio and Bookinfo source
   ```
   make setup  
   ```
1. Review a single service: ratings
   ```
   cd src/ratings
   less ratings.js
   ```
1. Download npm modules
   ```
   npm install
   ```
1. Run ratings
   ```
   npm start 8000
   ```

1. Access http://localhost:8000
