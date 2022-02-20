# hse_hw1_meth


# Ссылка на коллаб
https://colab.research.google.com/drive/1yDofM1_mVR0kWSLPY2NgrNuJbgXSAhMS?usp=sharing


# Часть 1
Будем смотреть по cell 8 (SRR5836473)

Можно заметить необычный GC-состав. 

На графике видно два пика, по сравнению с секвенированием РНК, там один пик соответсвтвующий нормальному распределению.

У нашего образца содержание Цитозина и Гуанина, ниже чем в РНК, Тимина – выше.


<img width="404" alt="fastqc1" src="https://user-images.githubusercontent.com/71277325/154861597-780da20c-4972-432f-b885-e7ef77bb152b.PNG">
<img width="515" alt="fastqc2" src="https://user-images.githubusercontent.com/71277325/154861613-ffad616d-4d1d-4418-827c-157610b5dd72.PNG">
<img width="542" alt="fastqc3" src="https://user-images.githubusercontent.com/71277325/154861617-f7358710-d77d-4dbe-90e8-c828c43ad7fd.PNG">

# Часть 2

## Сколько ридов пришлось на целевые регионы и дуплицированных чтений

| Образец | SRA | 11347700-11367700 | 40185800-40195800 | Duplicated, % | 
| ------------- | ------------- | ------------- | ------------- |  ------------- | 
| SRR5836473 | 8 cell | 1090 | 464 | 18.31 | 
| SRR3824222 | Epiblast | 2328 | 1062| 2.92 | 
| SRR5836475 | ICM | 1456 | 630 | 9.08 | 

html файлы в папке html


bash-скрипт для выполнения дедупликации для всех образцов одновременно
```
! ls *_1_bismark_bt2_pe.bam | xargs -P 4 -tI{} deduplicate_bismark  --bam  --paired  -o s_{} {}
```

## M-bias plot


Cамый большой процент CpG метилирования - около 77% - у Epiblast

Наименьший у ICM - около 23%

У cell 8 - около 43%

Можно заметить, что у всех образцов во втором в риде в начале чуть больший или меньший процент метилирования.

Также у всех образцов во втором риде процент метиляции для общего числа вызов СHH падает
### 8 cell

<img width="909" alt="8cell1" src="https://user-images.githubusercontent.com/71277325/154860565-e107db73-f854-45dd-89a9-5e8e95f02f26.PNG">

<img width="916" alt="8cell2" src="https://user-images.githubusercontent.com/71277325/154860569-2a745354-431f-4a75-af93-718f48676847.PNG">


### Epiblast

<img width="915" alt="epiblast1" src="https://user-images.githubusercontent.com/71277325/154860573-31e09c1b-fcb6-4404-aaba-8867b4b6c460.PNG">

<img width="893" alt="epiblast2" src="https://user-images.githubusercontent.com/71277325/154860577-d279aae1-4a95-4aee-a581-864fc96fcc61.PNG">


### ICM

<img width="897" alt="icm1" src="https://user-images.githubusercontent.com/71277325/154860582-2474a070-2c40-4924-bfcd-5cee15e06dc6.PNG">

<img width="908" alt="icm2" src="https://user-images.githubusercontent.com/71277325/154860589-2cba65ce-92da-4909-ae8d-d636e4e6297b.PNG">



## Гистограммы с общим уровнем метелирования
```
sra = ['3824222', '5836475',  '5836473']
for a in sra:
  name = 's_SRR' + a + '_1_bismark_bt2_pe.deduplicated.bedGraph'
  a = pd.read_csv(name, delimiter='\t', skiprows=1, header=None)
  plt.title('Распределение метилирования для %s' % kod) 
  plt.hist(a[3], bins=100, density=True)
  plt.xlabel('Процент метилированных цитозинов')
  plt.ylabel('Частота')
  plt.show()
```

### 8 cell

<img width="540" alt="5836473" src="https://user-images.githubusercontent.com/71277325/154860145-86406460-4622-44ca-8dc3-c885d0489ea0.png">

### Epiblast

<img width="540" alt="3824222" src="https://user-images.githubusercontent.com/71277325/154860163-83aed5cf-6db4-4707-aa01-d19ef6eb604f.png">

### ICM

<img width="540" alt="5836475" src="https://user-images.githubusercontent.com/71277325/154860179-cee04ec3-6e88-454a-9246-6e8315c44868.png">



## Визуализируйте уровень метилирования и покрытия для каждого образца 

![image_all](https://user-images.githubusercontent.com/71277325/154860899-8c676f88-d79d-4818-8ce6-d2e7b896bc4f.png)
![image_short](https://user-images.githubusercontent.com/71277325/154860903-fe9a2567-b818-4104-a371-63e50b78cdab.png)



