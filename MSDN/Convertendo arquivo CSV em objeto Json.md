# Convertendo arquivo CSV em objeto Json

Hoje em dia voc� pode fazer qualquer tipo de aplicativo ou software que ajuda a sua empresa e eu aqui
morando fora do Brasil n�o � diferente. A empresa precisa converter um arquivo do tipo
csv em dados que podem ser pesquisados e trabalhados.

**O que � um arquivo csv?**
- � um arquivo de dados que � basicamente separado por v�rgula. Normalmente a primeira linha possui
as colunas e depois da primeira vem os dados.

O que eu preciso fazer � pegar todos os dados desse arquivo e converter em um formato string
muito simples que utilizamos hoje em dia chamado Json. Json � JavaScript Object Notation que 
basicamente cont�m strings com chave e valor.

Veja um exemplo b�sico de um Json:

	{
		"Nome" : "Mauricio Junior",
		"Site" : "https://www.mauriciojunior.net
	}
Code: 1.1 - Json Simples

Ent�o vamos l�, como eu fa�o para converter qualquer tipo de arquivo CSV em Json? O c�digo 
� simples e f�cil porque eu preciso fazer um split por v�rgula.

    public static string ConverterCsvParaJson(string path)
    {
        var csv = new List<string[]>();
        var lines = File.ReadAllLines(path);

        foreach (string line in lines)
            csv.Add(line.Split(','));

        var properties = lines[0].Split(',');

        var listObjResult = new List<Dictionary<string, string>>();

        for (int i = 1; i < lines.Length; i++)
        {
            var objResult = new Dictionary<string, string>();
            for (int j = 0; j < properties.Length; j++)
                objResult.Add(properties[j], csv[i][j]);

            listObjResult.Add(objResult);
        }

        return JsonConvert.SerializeObject(listObjResult);
    }

Note que o primeiro passo � ler todas as linhas do arquivo. Depois disso separar as linhas pela 
v�rgula. Transformar em um dicion�rio, depois colocar os valores dentro desse dicion�rio e 
para terminar � necess�rio fazer uma serializa��o do objeto criado usando o using Newtonsoft.Json.

Espero que tenha gostado e qualquer d�vida por entrar em contato comigo pelo site [https://www.mauriciojunior.net](https://www.mauriciojunior.net).