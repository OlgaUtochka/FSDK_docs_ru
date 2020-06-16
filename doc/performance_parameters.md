# Параметры производительности

В данном пункте используются следующие сокращения:
* FAR (false accept rate) – вероятность ложного сопоставления с объектом в базе.
* TAR (true accept rate) – вероятность корректного сопоставления с объектом в базе.
* FRR (false reject rate) – вероятность ложного отказа в доступе объекту, который есть в базе.
* IR (identification rate) – вероятность идентификации.

## Характеристики идентификации

### Временные характеристики для Core i7 4.5 ГГц

<table cellpadding ="5" border="1" style="border-collapse:collapse;center">
<tr>
  <th rowspan=3>Метод распознавания</th>
  <th rowspan=3>Создание шаблона (мс)</th>
  <th colspan=6>Поиск среди N шаблонов (мс)</th>
  <th rowspan=3>Сравнение шаблонов (мс)</th>
</tr>
<tr>
  <th colspan=3>Без ускорения</th>
  <th colspan=3>Ускоренный</th>
</tr>
<tr>
  <th>N = 10<sup>4</sup> </th>
  <th>N = 10<sup>6</sup> </th>
  <th>N = 10<sup>7</sup> </th>
  <th>N = 10<sup>4</sup> </th>
  <th>N = 10<sup>6</sup> </th>
  <th>N = 10<sup>7</sup> </th>
</tr>
<tr align="center"> <th align="center"> 6      </th>    <td>  35 (50*)  </td>  <td> 0.22</td> <td> 34.2 </td> <td> 340 </td>  <td> 0.22</td> <td> 34.2 </td> <td> 340 </td>  <td>0.00008</td>  </tr>
<tr align="center"> <th align="center"> 6.2    </th>    <td>  35 (50*)  </td>  <td> 0.22</td> <td> 34.2 </td> <td> 340 </td>  <td> 0.22</td> <td> 34.2 </td> <td> 340 </td>  <td>0.00008</td>  </tr>
<tr align="center"> <th align="center"> 6.3    </th>    <td>  35 (50*)  </td>  <td> 0.22</td> <td> 34.2 </td> <td> 340 </td>  <td> 0.22</td> <td> 34.2 </td> <td> 340 </td>  <td>0.00008</td>  </tr>
<tr align="center"> <th align="center"> 6.4    </th>    <td>  35 (50*)  </td>  <td> 0.22</td> <td> 34.2 </td> <td> 340 </td>  <td> 0.22</td> <td> 34.2 </td> <td> 340 </td>  <td>0.00008</td>  </tr>
<tr align="center"> <th align="center"> 6.5    </th>    <td>  35 (50*)  </td>  <td> 2.95</td> <td> 296  </td> <td> 2880</td>  <td> 0.43</td> <td> 16.1 </td> <td> 165 </td>  <td>0.06   </td>  </tr>
<tr align="center"> <th align="center"> 6.6    </th>    <td>  50 (55*)  </td>  <td> 1.22</td> <td> 131  </td> <td> 1310</td>  <td> 0.25</td> <td> 12.1 </td> <td> 126 </td>  <td>0.04   </td>  </tr>
<tr align="center"> <th align="center"> 6.7    </th>    <td>  40 (45*)  </td>  <td> 1.22</td> <td> 131  </td> <td> 1310</td>  <td> 0.25</td> <td> 12.1 </td> <td> 126 </td>  <td>0.04   </td>  </tr>
<tr align="center"> <th align="center"> 7      </th>    <td> 210 (290*) </td>  <td> 0.22</td> <td> 34.2 </td> <td> 340 </td>  <td> 0.22</td> <td> 34.2 </td> <td> 340 </td>  <td>0.00008</td>  </tr>
<tr align="center"> <th align="center"> 7.2    </th>    <td> 210 (290*) </td>  <td> 0.22</td> <td> 34.2 </td> <td> 340 </td>  <td> 0.22</td> <td> 34.2 </td> <td> 340 </td>  <td>0.00008</td>  </tr>
<tr align="center"> <th align="center"> 7.3    </th>    <td> 210 (290*) </td>  <td> 2.95</td> <td> 296  </td> <td> 2880</td>  <td> 0.43</td> <td> 16.1 </td> <td> 165 </td>  <td>0.06   </td>  </tr>
<tr align="center"> <th align="center"> 7.6    </th>    <td> 210 (290*) </td>  <td> 1.22</td> <td> 131  </td> <td> 1310</td>  <td> 0.25</td> <td> 12.1 </td> <td> 126 </td>  <td>0.04   </td>  </tr>
<tr align="center"> <th align="center"> 7.7    </th>    <td> 170 (180*) </td>  <td> 1.22</td> <td> 131  </td> <td> 1310</td>  <td> 0.25</td> <td> 12.1 </td> <td> 126 </td>  <td>0.04   </td>  </tr>
<tr align="center"> <th align="center"> 8.6    </th>    <td>  20 (20*)  </td>  <td> 1.22</td> <td> 131  </td> <td> 1310</td>  <td> 0.25</td> <td> 12.1 </td> <td> 126 </td>  <td>0.04   </td>  </tr>
<tr align="center"> <th align="center"> 8.7    </th>    <td>  20 (20*)  </td>  <td> 1.22</td> <td> 131  </td> <td> 1310</td>  <td> 0.25</td> <td> 12.1 </td> <td> 126 </td>  <td>0.04   </td>  </tr>
<tr align="center"> <th align="center"> 9.30   </th>    <td>  30        </td>  <td> 0.60</td> <td> 64.2 </td> <td> 643 </td>  <td> 0.18</td> <td> 12.0 </td> <td> 117 </td>  <td>0.04   </td>  </tr>
<tr align="center"> <th align="center"> 9.300  </th>    <td> 260        </td>  <td> 0.60</td> <td> 64.2 </td> <td> 643 </td>  <td> 0.18</td> <td> 12.0 </td> <td> 117 </td>  <td>0.04   </td>  </tr>
<tr align="center"> <th align="center"> 9.1000 </th>    <td> 730        </td>  <td> 0.60</td> <td> 64.2 </td> <td> 643 </td>  <td> 0.18</td> <td> 12.0 </td> <td> 117 </td>  <td>0.04   </td>  </tr>
</table>

\* – время создания шаблона при параметре `processing_less_memory_consumption` с установленным значением `true` при вызове метода `FacerecService.createRecognizer` для создания распознавателя.

**Примечания:**
* Время ускоренного поиска приведено для `k=1`, при больших значениях `k` время будет увеличиваться до времени поиска без ускорения.
* Ускоренный поиск реализован только для методов распознавания 6.5, 6.6, 6.7, 7.3, 7.6, 7.7, 8.6, 8.7, 9.30, 9.300, 9.1000.
* Для достижения этих скоростей шаблоны в индексе дожны быть расположены в порядке их создания (через метод `Recognizer.processing` или `Recognizer.loadTemplate`).
