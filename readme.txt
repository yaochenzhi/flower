Flower - Celery monitoring tool
Flower is a web based tool for monitoring and administrating Celery clusters

https://flower.readthedocs.io/en/latest/


[ Features ]
    Real-time monitoring using Celery Events
    Remote Control
    Broker monitoring
    HTTP API
    Basic Auth, GitHub OAuth2 and Google OpenID authentication

[ Task filter ]
    test_search.py

[ REST API ]
    GET /api/workers HTTP/1.1
    POST /api/worker/shutdown/celery@worker2 HTTP/1.1
    POST /api/worker/pool/restart/celery@worker2 HTTP/1.1
    POST /api/worker/pool/grow/celery@worker2?n=3 HTTP/1.1
    POST /api/worker/pool/shrink/celery@worker2 HTTP/1.1
    POST /api/worker/pool/autoscale/celery@worker2?min=3&max=10 HTTP/1.1
    POST /api/worker/queue/add-consumer/celery@worker2?queue=sample-queue
    POST /api/worker/queue/cancel-consumer/celery@worker2?queue=sample-queue
    GET /api/tasks HTTP/1.1
    GET /api/task/types HTTP/1.1
    GET /api/task/info/91396550-c228-4111-9da4-9d88cfd5ddc6 HTTP/1.1
    POST /api/task/apply/tasks.add HTTP/1.1
    POST /api/task/async-apply/tasks.add HTTP/1.1
    POST /api/task/send-task/tasks.add HTTP/1.1
    GET /api/task/result/c60be250-fe52-48df-befb-ac66174076e6 HTTP/1.1
    POST /api/task/abort/c60be250-fe52-48df-befb-ac66174076e6 HTTP/1.1
    POST /api/task/timeout/tasks.sleep HTTP/1.1
    POST /api/task/rate-limit/tasks.sleep HTTP/1.1
    POST /api/task/revoke/1480b55c-b8b2-462c-985e-24af3e9158f9?terminate=true


[ Authentication ]
    - HTTP Basic Authentication
        celery flower --basic_auth=user1:password1,user2:password2

    - Google OAuth 2.0
        celery flower -A celery_task --address=0.0.0.0 --port=80  --auth="yaochen..@gmail" --oauth2_key="...apps.googleusercontent.com" -oauth2_secret="xxxxx" --oauth2_redirect_uri="http://hahatest.com/login"

        export FLOWER_OAUTH2_KEY=...
        export FLOWER_OAUTH2_SECRET=...
        export FLOWER_OAUTH2_REDIRECT_URI=http://flower.example.com/login
        celery flower --auth=.*@example\.com

    - GitHub OAuth
        export FLOWER_OAUTH2_KEY=7956724aafbf5e1a93ac
        export FLOWER_OAUTH2_SECRET=f9155f764b7e466c445931a6e3cc7a42c4ce47be
        export FLOWER_OAUTH2_REDIRECT_URI=http://localhost:5555/login
        celery flower --auth_provider=flower.views.auth.GithubLoginHandler --auth=.*@example\.com

    ***
    Google OAuth
        https://developers.google.com/identity/sign-in/web/sign-in
        Authorized JavaScript origins
        yourflowerhost.domain
        Authorized redirect URIs
        yourflowerhost.domain/login

        To avoid
        400. That’s an error.
        Error: redirect_uri_mismatch
        
        The flower server need to able to connect to the Google server.

