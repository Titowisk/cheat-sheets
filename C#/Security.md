## Security

### Passwords
Guardando em texto puro definitivamente não é seguro.

Usando algoritmos de encriptagem? evita certos problemas. Mas o hash gerado por uma determinada palavra é sempre a mesma. Então se um atacante pegar uma lista das senhas
mais comuns e passar por encriptagem? ele pode acabar descobrindo o algoritmo utilizado. (partindo do pressuposto que ele possua acesso ao banco claro)

Usando um salt, duas palavras iguais irão gerar hashs diferentes. O que é mais seguro.

Fontes:

https://medium.com/dealeron-dev/storing-passwords-in-net-core-3de29a3da4d2#:~:text=BCrypt%20and%20PBKDF2%20are%20both,slower%20the%20algorithm%2C%20the%20better.
