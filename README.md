# hse_hw2_chip

Ссылка на колаб: https://colab.research.google.com/drive/1MvsmAbRUoYxtKgfSDmE3ImNxDRdia0_V?usp=sharing

# Основная часть

Я взял гистоновую линию HUES48 с гистоновой меткой H3K27me3. 

Реплика 1: ENCFF090UYV	

Реплика 2: ENCFF815LPM	

Файл контроля: ENCFF693RXC

## Отчеты FastQC

### ENCFF090UYV

Подрезания не потребовалось

![ENCFF090UYV](https://github.com/Deuqz/hse_hw2_chip/blob/master/pictures/ENCFF090UYV.png)

### ENCFF815LPM

Подрезания не потребовалось

![ENCFF815LPM](https://github.com/Deuqz/hse_hw2_chip/blob/master/pictures/ENCFF815LPM.png)

### ENCFF693RXC

Per sequence quality хуже по сравнению с репликами, однако подрезания ничего не дали, поэтому оставил обычный файл.
Добавил вариант подрезанного файла в артефакты.

![ENCFF693RXC](https://github.com/Deuqz/hse_hw2_chip/blob/master/pictures/ENCFF693RXC.png)

Подрезание выполнялось командой

```
!trimmomatic SE -phred33 ENCFF693RXC.fastq ENCFF693RXC_trimmed.fastq ILLUMINACLIP:TruSeq3-SE:2:30:10 \
  LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36
!./FastQC/fastqc ENCFF693RXC_trimmed.fastq
```

## Таблица результатов bowtie

| Образец         | Количество чтений | Невыровненные чтения | Уникально выровненные чтения | Неуникально выровненные чтения |
|-----------------|-------------------|----------------------|------------------------------|--------------------------------|
| ENCFF090UYV     | 43763763          | 39692520 (90.70%)    | 1144629 (2.62%)              | 2926614 (6.69%)                |
| ENCFF815LPM     | 33979765          | 29585894 (87.07%)    | 1201637 (3.54%)              | 3192234 (9.39%)                |
| ENCFF693RXC     | 42675605          | 35483816 (83.15%)    | 1790757 (4.20%)              | 5401032 (12.66%)               |

Видим довольно низкое количество выровненных чтений. Все из-за того, что выравнивались только на одну хромосому.

## Диаграммы Венна

![venn11](https://github.com/Deuqz/hse_hw2_chip/blob/master/pictures/venn11.jpg)

![venn12](https://github.com/Deuqz/hse_hw2_chip/blob/master/pictures/venn12.jpg)

![venn21](https://github.com/Deuqz/hse_hw2_chip/blob/master/pictures/venn21.jpg)

![venn22](https://github.com/Deuqz/hse_hw2_chip/blob/master/pictures/venn22.jpg)

Мы получили пики только для выравнивания на одну хромосому, а в референсном файле должны быть пики для всех хромосом,
поэтому в нем сильно больше пиков. Для каждой реплики у нас суммарно около 1000 пересечений. 