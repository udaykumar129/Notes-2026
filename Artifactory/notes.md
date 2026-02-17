# Clean up notes

- Git URL : https://gitlab.logistics.corp/weshahm/artifactory-clean-up.git
- Clone the project into your local and checkout v2 branch
- Use this and generate password by puttin username:password in Base64 code in URL
- https://mixedanalytics.com/tools/basic-authentication-generator/
- Then put this code as Authorization "Basic code" - In Place of Code put the generated password ( use this YWRtaW46UGFzc3dvcmQx )
- Then run node query.js…This will give us list of all images in artifactory
- Collet images of all projects from K8s clusters:
- Run this command all clusters to collect docker image versions that we need to keep
  
`kubectl get pods --all-namespaces -o=jsonpath='{range .items[*]}{"\n"}{range .spec.containers[*]}{.image}{end}{end}' -l 'app.kubernetes.io/name in (cjf-app,cjf-rest-app,cjf-react-app,cal-app)' | cut -d'/' -f2 | awk '{split($0,a,":"); print a[1],a[2]}' >> all-cjf-versions.csv`
- Run this command to remove duplicates and sort by the app name
- cat all-cjf-versions.csv| sort -u -k1 > all-cjf-versions-sorted.csv
