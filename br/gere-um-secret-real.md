Gere um secret real
segurança
Garanta que sua aplicação em produção esteja usando uma chave custimozada. Cheque isto no arquivo `app/config/parameters.yml`:

    secret:  please_use_a_real_secret_here

Por padrão a "secret" *não* é verdadeiramente secreta, você *precisa* mudá-la por uma aleatória.
