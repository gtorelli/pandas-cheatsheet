### Ler dados CSV
data = pd.read_csv('my_file.csv')  
data = pd.read_csv('my_file.csv', sep=';', encoding='latin-1', nrows=1000, skiprows=[2,5])  

### Checar Dados
data.shape  
data.describe()  

### Calcular média
print(s.sum()/s.count())  

### Visualizar Dados
5 primeiras linhas: Data.head(5)  
Colunas: data.loc[8]  
Oitavo valor da coluna_1: data.loc[8, 'column_1']  

### Move linha 4 para 6
data.loc[range(4,6)]  

### Adiciona Coluna com índice específico
starts at zero  
position = 1  
column_name = 'gender'  
column_data = pd.Series(['female','male','male'])  
df.insert(position, column_name, column_data)  

### Adiciona Coluna
states = pd.Series(['dc','ca','ny'])  
df['state'] = states  

### Apaga  Colunas
df.drop(columns=['age','name'],inplace=True)  

specify the axis=0 for row, and axis=1 for column.  

DF.drop('d', axis=0)  
DF.drop('column', axis=1)  

### Filtros com operadores lógicos
& (AND)  
~ (NOT)  
| (OR)  
data[data['column_1']=='french']  
data[(data['column_1']=='french') & (data['year_born']==1990)]  
data[(data['column_1']=='french') & (data['year_born']==1990) & ~(data['city']=='London')]  

### Subset com sin  
data[data['column_1'].isin(['french', 'english'])]  

### Subset removendo duplicados  
d001 = dfbolhas.drop_duplicates(subset='frame', keep="first")  

### Subset com iloc  
linhas -> df.iloc[0, 1]  
range -> df.iloc[0:3]  

### Renomeia coluna  
dfgotas = dfgotas.rename(columns={"diamEquivFA[mm]": "diamEquivFA[GOTAS]"})  

### Copia dataframe  
df2 = df1.copy()  

### Substitui valores na coluna
level_map = {1: 'high', 2: 'medium', 3: 'low'}  
df['c_level'] = df['c'].map(level_map)  

### Mostra tipo das variáveis
df.select_dtypes(include=['float64', 'int64'])  

### Criar nova coluna a partir de outras colunas utilizando uma função para filtro
def rule(x, y):  
    if x == 'high' and y > 10:  
         return 1  
    else:  
         return 0df = pd.DataFrame({ 'c1':[ 'high' ,'high', 'low', 'low'], 'c2': [0, 23, 17, 4]})  

df['new'] = df.apply(lambda x: rule(x['c1'], x['c2']), axis =  1)  
df.head()

### Máximo valor de duas colunasn
df['maximum'] = df[['c1','c2']].max(axis =1)  

### Mostra o estado ordenado pela coluna 'c'
df['c'].value_counts().sort_index()

### Conta os valores
df['c'].value_counts()

### Conta quantos valores faltantes
import pandas as pd  
import numpy as np  

df = pd.DataFrame({ 'id': [1,2,3], 'c1':[0,0,np.nan], 'c2': [np.nan,1,1]})  
df = df[['id', 'c1', 'c2']]  
df['num_nulls'] = df[['c1', 'c2']].isnull().sum(axis=1)  
df.head()  

### Selecionar linhas com ID especifico
df_filter = df['ID'].isin(['A001','C022',...])  
df[df_filter]  

### Separar por ponto de corte do Percentil
import numpy as np  
cut_points = [np.percentile(df['c'], i) for i in [50, 80, 95]]  
df['group'] = 1  
for i in range(3):  
    df['group'] = df['group'] + (df['c'] < cut_points[i])  
#or <= cut_points[i]  

### Exporta para CSV
data.to_csv('my_new_file.csv', index=None)  

### Enviar as 5 primeiras linhas para um arquivo CSV
print(df[:5].to_csv())  

### Plot Básico
Linha->         data['column_numerical'].plot()  
Histograma->     data['column_numerical'].hist()  

### Troca o valor da oitava linha da 'coluna_1' por 'english'
data.loc[8, 'column_1'] = 'english'  

### Troca todas as linhas da coluna de 'french' para 'French'
data.loc[data['column_1']=='french', 'column_1'] = 'French'  

### Conta ocorrências de uma coluna especifica
data['column_1'].value_counts()  

### Aplica função len() para cada elemento da 'coluna_1'
data['column_1'].map(len)  

### Aplica operação para cada elemento da 'coluna_1'
data['column_1'].map(len).map(lambda x: x/100).plot()  

### Correlação e Scatterplot
data.corr()  
data.corr().applymap(lambda x: int(x*100)/100)  

pd.plotting.scatter_matrix(data, figsize=(12,8))  

### JOIN (Adiciona um df em outro)
data.merge(other_data, on=['column_1', 'column_2', 'column_3']) 

### GROUP (Agrupa usando coluna de referência)
data.groupby('column_1')['column_2'].apply(sum).reset_index()  

### Converte coluna para o tipo data
df = pd.DataFrame({'name': ['alice','bob','charlie'], date_of_birth': ['27/05/2001','16/02/1999','25/09/1998']})  

[['name','date_of_birth']]df['date_of_birth'] = pd.to_datetime(df['date_of_birth'],format='%d/%m/%Y')  

### Utilizando funções
def segmentMatch(TimeCol, ResponseCol):  
  result = TimeCol/ResponseCol  
return result  

df['NewCol'] = df.apply(lambda x: segmentMatch(x['TimeCol'], x['ResponseCol']), axis=1)  

### Comprimir dataset reduzindo espaço em disco
df.to_csv('random_data.gz', compression='gzip', index=False)

df = pd.read_csv('random_data.gz')

### Preenche valores faltantes com zero:
df.fillna(0)

### Preenche valores faltantes com valor anterior
df.fillna(method='bfill')

### Preenche valores faltantes com proximo valor
df.fillna(method='ffill')

### SITES E TUTORIAIS
https://towardsdatascience.com/10-python-pandas-tricks-that-make-your-work-more-efficient-2e8e483808ba  
https://towardsdatascience.com/be-a-more-efficient-data-scientist-today-master-pandas-with-this-guide-ea362d27386  
http://queirozf.com/entries/pandas-dataframe-examples-column-operations  

