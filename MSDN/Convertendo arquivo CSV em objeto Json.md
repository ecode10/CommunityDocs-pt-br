# Convertendo arquivo CSV em objeto Json

Hoje em dia você pode fazer qualquer tipo de aplicativo ou software que ajuda a sua empresa e eu aqui
morando fora do Brasil não é diferente. A empresa precisa converter um arquivo do tipo
csv em dados que podem ser pesquisados e trabalhados.

**O que é um arquivo csv?**
- É um arquivo de dados que é basicamente separado por vírgula. Normalmente a primeira linha possui
as colunas e depois da primeira vem os dados.

O que eu preciso fazer é pegar todos os dados desse arquivo e converter em um formato string
muito simples que utilizamos hoje em dia chamado Json. Json é JavaScript Object Notation que 
basicamente contém strings com chave e valor.

Veja um exemplo básico de um Json:

	{
		"Nome" : "Mauricio Junior",
		"Site" : "https://www.mauriciojunior.net
	}
Code: 1.1 - Json Simples

Então vamos lá, como eu faço para converter qualquer tipo de arquivo CSV em Json? O código 
é simples e fácil porque eu preciso fazer um split por vírgula.

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

Note que o primeiro passo é ler todas as linhas do arquivo. Depois disso separar as linhas pela 
vírgula. Transformar em um dicionário, depois colocar os valores dentro desse dicionário e 
para terminar é necessário fazer uma serialização do objeto criado usando o using Newtonsoft.Json.

Espero que tenha gostado e qualquer dúvida por entrar em contato comigo pelo site [https://www.mauriciojunior.net](https://www.mauriciojunior.net).