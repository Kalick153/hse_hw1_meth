# hse_hw1_meth


# Ссылка на коллаб
https://colab.research.google.com/drive/1yDofM1_mVR0kWSLPY2NgrNuJbgXSAhMS?usp=sharing


# Часть 1


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

## Гистограммы с общим уровнем метелирования
### 8 cell

<img width="540" alt="5836473" src="https://user-images.githubusercontent.com/71277325/154860145-86406460-4622-44ca-8dc3-c885d0489ea0.png">

### Epiblast

<img width="540" alt="3824222" src="https://user-images.githubusercontent.com/71277325/154860163-83aed5cf-6db4-4707-aa01-d19ef6eb604f.png">

### ICM

<img width="540" alt="5836475" src="https://user-images.githubusercontent.com/71277325/154860179-cee04ec3-6e88-454a-9246-6e8315c44868.png">



## Рисунки с уровнем метилирования и покрытием на любом регионе 
