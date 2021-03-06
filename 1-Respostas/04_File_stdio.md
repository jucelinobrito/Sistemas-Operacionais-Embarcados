Para todas as questões, utilize as funções da biblioteca `stdio.h` de leitura e de escrita em arquivo (`fopen()`, `fclose()`, `fwrite()`, `fread()`, dentre outras). Compile os códigos com o gcc e execute-os via terminal.

1. Crie um código em C para escrever "Ola mundo!" em um arquivo chamado 'ola_mundo.txt'.
```C
#include<stdio.h>
#include<stdlib.h>

	void main()
	{
		FILE *fp;
		fp = fopen("arquivo.txt", "w");

		if (!fp)
		{
			printf("Erro na leitura do arquivo.");
			exit(0);
		}

		fprintf(fp, "ola mundo");
		fclose(fp);
		return 0;
	}
```
2. Crie um código em C que pergunta ao usuário seu nome e sua idade, e escreve este conteúdo em um arquivo com o seu nome e extensão '.txt'. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_1':

```bash
$ ./ola_usuario_1
$ Digite o seu nome: Eu
$ Digite a sua idade: 30
$ cat Eu.txt
$ Nome: Eu
$ Idade: 30 anos
```

```C
#include<stdio.h>
#include<stdlib.h>
#include <string.h>

	void main()
	{
		char nome[20];
		int idade;
		printf("Digite o seu nome:\n");
		//gets(nome);
		scanf("%s", nome);
		printf("Digite sua idade:\n");
		scanf("%d", &idade);
		FILE *fp;
		char nova[20]="";	
		strcat(nova,nome);
		strcat(nova,".txt");
		fp = fopen(nova, "w");

		if (!fp)
		{
			printf("Erro na leitura do arquivo.");
			exit(0);
		}

		fprintf(fp,"Nome: %s\n",nome);
		fprintf(fp,"Idade: %d\n",idade);
		fclose(fp);
	}
```

3. Crie um código em C que recebe o nome do usuário e e sua idade como argumentos de entrada (usando as variáveis `argc` e `*argv[]`), e escreve este conteúdo em um arquivo com o seu nome e extensão '.txt'. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_2':

```bash
$ ./ola_usuario_2 Eu 30
$ cat Eu.txt
$ Nome: Eu
$ Idade: 30 anos
```

```C
#include<stdio.h>
#include<stdlib.h>
#include <string.h>

	int main(int argc, const char **argv)
	{
		FILE *fp;
		char nova[20]="";
		strcat(nova,argv[1]);
		strcat(nova,".txt");
		fp = fopen(nova, "w");

		if (!fp)
		{
			printf("Erro na leitura do arquivo.");
			exit(0);
		}

		fprintf(fp,"Nome: %s\n",argv[1]);
		fprintf(fp,"Idade: %s\n",argv[2]);
		fclose(fp);
		return 0;
	}
```

4. Crie uma função que retorna o tamanho de um arquivo, usando o seguinte protótipo: `int tam_arq_texto(char *nome_arquivo);` Salve esta função em um arquivo separado chamado 'bib_arqs.c'. Salve o protótipo em um arquivo chamado 'bib_arqs.h'. Compile 'bib_arqs.c' para gerar o objeto 'bib_arqs.o'.
```C
#include<stdio.h>
#include<stdlib.h>
#include <string.h>

	long int tam_arq_texto(char *nome_arquivo)
	{
		FILE *fp;
		long int tamanho=0;
		fp = fopen(nome_arquivo,"rb");
		if (!fp)
		{
			printf("Erro na leitura do arquivo.");
			exit(0);
		}
		fseek(fp,0,SEEK_END);
		tamanho = ftell(fp);
		return tamanho;
	}

int main(){
	char *nome;
	scanf("%s", nome);	
	long int saize = tam_arq_texto(nome);
	printf("%ld\n",saize);


	return 0;


}
```
5. Crie uma função que lê o conteúdo de um arquivo-texto e o guarda em uma string, usando o seguinte protótipo: `char* le_arq_texto(char *nome_arquivo);` Repare que o conteúdo do arquivo é armazenado em um vetor interno à função, e o endereço do vetor é retornado ao final. (Se você alocar este vetor dinamicamente, lembre-se de liberar a memória dele quando acabar o seu uso.) Salve esta função no mesmo arquivo da questão 4, chamado 'bib_arqs.c'. Salve o protótipo no arquivo 'bib_arqs.h'. Compile 'bib_arqs.c' novamente para gerar o objeto 'bib_arqs.o'.

```C
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

char *le_arq_texto(char* nome_arquivo)
{
		FILE *fp;
		char *name;
		name= (char *) malloc(100*sizeof(char));
		fp = fopen(nome_arquivo,"rb");
		if (!fp)
		{
			printf("Erro na leitura do arquivo.");
			exit(0);
		}
		fread(&name[0],sizeof(double),sizeof(char),fp);
		return name;
		free(name);
	}

int main()
{
	char arquivo[100];
	scanf("%s", arquivo);
	printf("%s\n", le_arq_texto(arquivo));	
	return 0;
}
```

6. Crie um código em C que copia a funcionalidade básica do comando `cat`: escrever o conteúdo de um arquivo-texto no terminal. Reaproveite as funções já criadas nas questões anteriores. Por exemplo, considerando que o código criado recebeu o nome de 'cat_falsificado':

```bash
$ echo Ola mundo cruel! Ola universo ingrato! > ola.txt
$ ./cat_falsificado ola.txt
$ Ola mundo cruel! Ola universo ingrato!
```
```C
#include<stdio.h>
#include<stdlib.h>
#include<string.h>

char *cat_falsificado(char* nome_arquivo)
{
		FILE *fp;
		char *name;
		name= (char *) malloc(100*sizeof(char));
		fp = fopen(nome_arquivo,"rb");
		if (!fp)
		{
			printf("Erro na leitura do arquivo.");
			exit(0);
		}
		fread(&name[0],sizeof(double),sizeof(char),fp);
		return name;
		free(name);
	}

int main()
{
	char arquivo[100];
	scanf("%s", arquivo);
	printf("%s\n", cat_falsificado(arquivo));	
	return 0;
}
```
7. Crie um código em C que conta a ocorrência de uma palavra-chave em um arquivo-texto, e escreve o resultado no terminal. Reaproveite as funções já criadas nas questões anteriores. Por exemplo, considerando que o código criado recebeu o nome de 'busca_e_conta':

```bash
$ echo Ola mundo cruel! Ola universo ingrato! > ola.txt
$ ./busca_e_conta Ola ola.txt
$ 'Ola' ocorre 2 vezes no arquivo 'ola.txt'.
```
