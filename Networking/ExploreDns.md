### Which of the below name can be used to access the payroll service from the test application?
웹페이지서 payroll을쳐서 통신이 되는지 확인 

### We just deployed a web server - webapp - that accesses a database mysql - server. However the web server is failing to connect to the database server. Troubleshoot and fix the issue.
### They could be in different namespaces. First locate the applications. The web server interface can be seen by clicking the tab Web Server at the top of your terminal.
### Web Server: webapp
### Uses the right DB_Host name
kubectl get pods webapp -o yaml > webapp.yaml
        env:
        - name: DB_Host
          value: mysql.payroll (이부분 수정)
kubectl apply -f webapp.yaml

### From the hr pod nslookup the mysql service and redirect the output to a file /root/CKA/nslookup.out
### nslookup output redirected
kubectl exec -it hr -- nslookup mysql.payroll > /root/CKA/nslookup.out
