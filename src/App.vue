<script>
  export default{
    data(){
      score: Array(30).fill().map((_, index) => `Item ${index +  1}`)
    }
  }
</script>

<template>
  <h2>Website Analyzer</h2>
  <br>
  <input class="URL" type="text" id="URL" name="URL">
  <br>
  <button type="button" @click="">Analyze</button>
  <br>
  <br>
  <table style="width:100%;">
        <tr>
            <td style="width:45%;">
              <div class="tooltip">1. Использование IP-адреса
                <span class="tooltiptext">Если в URL-адресе вместо доменного имени используется IP-адрес, например “http://125.98.3.123/fake.html”, пользователи могут быть уверены, что кто-то пытается украсть их личную информацию. Иногда IP-адрес преобразуется в шестнадцатеричный код, как показано в следующем примере ссылки: http://0x58.0xCC.0xCA.0x62/2/paypal.ca/index.html”. Если в URL-адресе найден IP, данная категория получает -1 балл, иначе 1.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">16. Server Form Handler (SFH)
                <span class="tooltiptext">SFH, содержащие пустую строку или “about:blank”, считаются сомнительными, поскольку в отношении предоставленной информации следует предпринять какие-либо действия. Кроме того, если доменное имя в SFHs отличается от доменного имени веб-страницы, это указывает на то, что веб-страница подозрительна, поскольку отправленная информация редко обрабатывается внешними доменами.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
            <td style="width:45%;">
              <div class="tooltip">2. Длинный URL
                <span class="tooltiptext">Фишеры могут использовать длинный URL-адрес, чтобы скрыть сомнительную часть в адресной строке. Чтобы обеспечить точность нашего исследования, мы рассчитали длину URL-адресов в наборе данных и получили среднюю длину URL-адреса. Результаты показали, что если длина URL-адреса больше или равна 54 символам, то URL-адрес классифицируется как фишинговый.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">17. Отправка информации на электронную почту
                <span class="tooltiptext">Веб-форма позволяет пользователю отправить свою личную информацию, которая направляется на сервер для обработки. Фишер может перенаправить информацию пользователя на электронную почту злоумышленника. С этой целью может использоваться язык сценариев на стороне сервера, такой как функция “mail()” в PHP. Еще одной клиентской функцией, которая может быть использована для этой цели, является функция “mailto:”.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
            <td style="width:45%;">
              <div class="tooltip">3. Использование сервисов сокращения URL-адресов “TinyURL”
                <span class="tooltiptext">Сокращение URL-адреса - это метод, при котором URL-адрес может быть значительно уменьшен по длине и по-прежнему вести на требуемую веб-страницу. Это достигается с помощью “HTTP-перенаправления” на короткое доменное имя, которое ссылается на веб-страницу с длинным URL. Например, URL-адрес “http://portal.hud.ac.uk/” можно сократить до “bit.ly/19DXSk4”.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">18. Аномальный URL-адрес
                <span class="tooltiptext">Эту функцию можно извлечь из базы данных WHOIS. Для легального веб-сайта идентификатор обычно является частью его URL.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
            <td style="width:45%;">
              <div class="tooltip">4. URL-адрес с символом “@”
                <span class="tooltiptext">Использование символа “@” в URL-адресе приводит к тому, что браузер игнорирует все, что предшествует символу “@”, и реальный адрес часто следует за символом “@”.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">19. Переадресация веб-сайта
                <span class="tooltiptext">Тонкая грань, отличающая фишинговые веб-сайты от легальных, заключается в том, сколько раз веб-сайт был переадресован. В нашем наборе данных мы обнаружили, что легальные веб-сайты содержат перенаправление максимум один раз. С другой стороны, фишинговые веб-сайты, содержащие эту функцию, перенаправляют не менее 4 раз.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
          <td style="width:45%;">
              <div class="tooltip">5. Перенаправление с помощью “//”
                <span class="tooltiptext">Наличие “//” в URL-пути означает, что пользователь будет перенаправлен на другой веб-сайт. Примером таких URL-адресов является: http://www.legitimate.com//http://www.phishing.com ”. Мы проверяем местоположение, где появляется “//”. Мы обнаруживаем, что если URL начинается с “HTTP”, это означает, что “//” должно отображаться в шестой позиции. Однако, если URL использует “HTTPS”, то “//” должно отображаться в седьмой позиции.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">20. Изменение строки состояния
                <span class="tooltiptext">Фишеры могут использовать JavaScript, чтобы показывать пользователям поддельный URL в строке состояния. Чтобы извлечь эту функцию, мы должны извлечь исходный код веб-страницы, в частности событие “onMouseOver”, и проверить, вносит ли оно какие-либо изменения в строку состояния.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
          <td style="width:45%;">
              <div class="tooltip">6. Добавление префикса или суффикса, разделенного знаком (-), к домену
                <span class="tooltiptext">Символ тире редко используется в законных URL-адресах. Фишеры, как правило, добавляют префиксы или суффиксы, разделенные знаком (-), к доменному имени, чтобы пользователи чувствовали, что имеют дело с законной веб-страницей. Например http://www.Confirme-paypal.com/.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">21. Отключение щелчка правой кнопкой мыши
                <span class="tooltiptext">Фишеры используют JavaScript для отключения функции щелчка правой кнопкой мыши, чтобы пользователи не могли просматривать и сохранять исходный код веб-страницы. Эта функция трактуется точно так же, как “Использование onMouseOver для скрытия ссылки”. Тем не менее, для этой функции мы выполним поиск события “event.button==2” в исходном коде веб-страницы и проверим, отключен ли щелчок правой кнопкой мыши.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
          <td style="width:45%;">
              <div class="tooltip">7. Поддомен и несколько поддоменов
                <span class="tooltiptext">Давайте предположим, что у нас есть следующая ссылка: http://www.hud.ac.uk/students/. Доменное имя может включать домены верхнего уровня с кодами стран (ccTLD), которыми в нашем примере является “uk”. Часть “ac” является сокращением от “academic”, комбинированное “ac.uk” называется доменом второго уровня (SLD), а “hud” - это фактическое название домена. Чтобы создать правило для извлечения этой функции, мы сначала должны исключить (www.) из URL, который сам по себе фактически является поддоменом. Затем мы должны удалить (ccTLD), если он существует. Наконец, мы подсчитываем оставшиеся точки. Если количество точек больше единицы, то URL классифицируется как “Подозрительный”, поскольку у него есть один поддомен. Однако, если точек больше двух, он классифицируется как “фишинговый”, поскольку у него будет несколько поддоменов. В противном случае, если URL-адрес не содержит поддоменов, мы присвоим этой функции статус “Легитимной”.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">22. Использование всплывающих окон
                <span class="tooltiptext">Необычно встретить законный веб-сайт, предлагающий пользователям предоставить свою личную информацию через всплывающее окно. С другой стороны, эта функция использовалась на некоторых законных веб-сайтах, и ее основная цель - предупредить пользователей о мошеннических действиях или транслировать приветственное сообщение.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
          <td style="width:45%;">
              <div class="tooltip">8. HTTPS (Hyper Text Transfer Protocol with Secure Sockets Layer)
                <span class="tooltiptext">Наличие HTTPS очень важно для создания впечатления легитимности веб-сайта, но этого явно недостаточно. Авторы в (Mohammad, Thabtah and McCluskey 2012) (Mohammad, Thabtah and McCluskey 2013) предлагают проверить сертификат, назначенный с помощью HTTPS, включая степень доверия эмитента сертификата и срок действия сертификата. Центры сертификации, которые неизменно входят в число наиболее заслуживающих доверия, включают: “GeoTrust, GoDaddy, Network Solutions, Thawte, Comodo, Doster и VeriSign”. Кроме того, протестировав наши наборы данных, мы обнаружили, что минимальный возраст авторитетного сертификата составляет два года.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">23. Использование IFrame
                <span class="tooltiptext">IFrame - это HTML-тег, используемый для отображения дополнительной веб-страницы в той, которая отображается в данный момент. Фишеры могут использовать тег “iframe” и сделать его невидимым, т.е. без границ фрейма. В связи с этим фишеры используют атрибут “frameBorder”, который заставляет браузер отображать визуальное разграничение.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
          <td style="width:45%;">
              <div class="tooltip">9. Срок регистрации домена
                <span class="tooltiptext">Основываясь на том факте, что фишинговый веб-сайт существует в течение короткого периода времени, мы считаем, что надежные домены регулярно оплачиваются на несколько лет вперед. В нашем наборе данных мы обнаружили, что самые долгие мошеннические домены использовались только в течение одного года.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">24. Возраст домена
                <span class="tooltiptext">Большинство фишинговых веб-сайтов существуют в течение короткого периода времени. Проанализировав наш набор данных, мы обнаружили, что минимальный возраст законного домена составляет 6 месяцев.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
          <td style="width:45%;">
              <div class="tooltip">10. Использование IP-адреса
                <span class="tooltiptext">Значок - это графическое изображение (иконка), связанное с определенной веб-страницей. Многие существующие пользовательские агенты, такие как графические браузеры и программы для чтения новостей, отображают значок в качестве визуального напоминания об идентификаторе веб-сайта в адресной строке. Если значок загружен с домена, отличного от указанного в адресной строке, то веб-страница, скорее всего, будет расценена как попытка фишинга.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">25. Запись DNS
                <span class="tooltiptext">Для фишинговых веб-сайтов либо заявленная идентификация не распознается базой данных WHOIS (Whois 2005), либо для имени хоста не создано записей (Pan and Ding 2006).</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
          <td style="width:45%;">
              <div class="tooltip">11. Использование нестандартного порта
                <span class="tooltiptext">Эта функция полезна для проверки того, работает ли определенная служба (например, HTTP) на определенном сервере. С целью контроля вторжений гораздо лучше просто открывать нужные вам порты. Несколько брандмауэров, прокси-серверов и серверов преобразования сетевых адресов (NAT) по умолчанию блокируют все или большинство портов и открывают только выбранные. Если открыты все порты, фишеры могут запускать практически любую службу, какую захотят, и в результате информация пользователя оказывается под угрозой.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">26. Трафик веб-сайта
                <span class="tooltiptext">Эта функция измеряет популярность веб-сайта, определяя количество посетителей и количество страниц, которые они посещают. Однако, поскольку фишинговые веб-сайты существуют в течение короткого периода времени, они могут не распознаваться базой данных Alexa (Alexa the Web Information Company., 1996). Проанализировав наш набор данных, мы обнаружили, что в худших сценариях легальные веб-сайты входят в топ-100 000. Кроме того, если домен не имеет трафика или не распознается базой данных Alexa, он классифицируется как “фишинговый”. В противном случае это классифицируется как “Подозрительное”.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
          <td style="width:45%;">
              <div class="tooltip">12. Наличие токена “HTTPS” в доменной части URL-адреса
                <span class="tooltiptext">Фишеры могут добавить токен “HTTPS” в доменную часть URL-адреса, чтобы обмануть пользователей. Например, http://https-www-paypal-it-webapps-mpp-home.soft-hair.com/</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">27. Рейтинг страницы
                <span class="tooltiptext">PageRank - это значение в диапазоне от “0” до “1”. PageRank предназначен для измерения важности веб-страницы в Интернете. Чем больше значение PageRank, тем важнее веб-страница. В наших наборах данных мы обнаружили, что около 95% фишинговых веб-страниц не имеют PageRank. Более того, мы обнаружили, что оставшиеся 5% фишинговых веб-страниц могут достигать значения PageRank вплоть до “0,2”.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
          <td style="width:45%;">
              <div class="tooltip">13. Request URL
                <span class="tooltiptext">URL-адрес запроса проверяет, загружены ли внешние объекты, содержащиеся на веб-странице, такие как изображения, видео и звуки, из другого домена. На законных веб-страницах адрес веб-страницы и большинство объектов, встроенных в веб-страницу, используют один и тот же домен.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">28. Индекс Google
                <span class="tooltiptext">Эта функция проверяет, находится ли веб-сайт в индексе Google или нет. Когда сайт индексируется Google, он отображается в результатах поиска (Webmaster resources, 2014). Обычно фишинговые веб-страницы доступны лишь в течение короткого периода времени, и в результате многие фишинговые веб-страницы могут быть недоступны в индексе Google.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
          <td style="width:45%;">
              <div class="tooltip">14. URL-адрес привязки
                <span class="tooltiptext">Привязка - это элемент, определенный тегом a. Эта функция обрабатывается точно так же, как “Запрос URL”. Однако для этой функции мы рассмотрим: 1. Если теги a и веб-сайт имеют разные доменные имена. Это аналогично функции request URL. 2. Если якорь не ссылается ни на какую веб-страницу.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">29. Количество ссылок, указывающих на страницу
                <span class="tooltiptext">Количество ссылок, указывающих на веб-страницу, указывает на уровень ее легитимности, даже если некоторые ссылки относятся к одному и тому же домену (Dean, 2014). В наших наборах данных и из-за их короткого срока службы мы обнаруживаем, что 98% элементов фишинговых наборов данных не содержат ссылок, указывающих на них. С другой стороны, на законных веб-сайтах есть как минимум 2 внешние ссылки, указывающие на них.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
        <tr>
          <td style="width:45%;">
              <div class="tooltip">15. Ссылки в тегах Meta, Script и Link
                <span class="tooltiptext">легальные веб-сайты обычно используют мета-теги для предоставления метаданных о HTML-документе; теги скриптов для создания клиентского скрипта; и теги ссылок для получения других веб-ресурсов. Ожидается, что эти теги связаны с одним и тем же доменом веб-страницы.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
            <td style="width:45%;">
              <div class="tooltip">30. Функция, основанная на статистических отчетах
                <span class="tooltiptext">Несколько сторон, таких как PhishTank (статистика PhishTank, 2010-2012) и StopBadware (StopBadware, 2010-2012), формируют многочисленные статистические отчеты о фишинговых веб-сайтах за каждый данный период времени; некоторые ежемесячно, а другие ежеквартально. В нашем исследовании мы использовали 2 формы статистики из первой десятки PhishTank: “Топ-10 доменов” и “Топ-10 IP-адресов” согласно статистическим отчетам, опубликованным за последние три года, начиная с января 2010 года по ноябрь 2012 года. В то время как для “StopBadware” мы использовали IP-адреса “Top 50”.</span>
              </div>
            </td>
            <td style="width:5%;">

            </td>
        </tr>
    </table>
</template>

<style scoped>
  table {
            border-collapse: collapse; /* Объединяет границы ячеек в одну линию */
        }
        td, th {
            border:  1px solid lightgray; /* Добавляет границу вокруг каждой ячейки */
            padding:  5px; /* Добавляет отступы внутри ячеек для удобства чтения */
        }

  button {
            width:  150px;
            margin-bottom: 10px;
            margin-top: 10px;
        }
  .tooltip {
      position: relative;
      display: inline-block;
      cursor: pointer;
  }

  .tooltip .tooltiptext {
      visibility: hidden;
      width:  500px;
      background-color: #555;
      color: #fff;
      text-align: center;
      padding:  5px  0;
      border-radius:  6px;

      position: absolute;
      z-index:  1;
      bottom:  100%; /* Позиционирование подсказки над элементом */
      left:  50%;
      margin-left: -60px; /* Центрирование подсказки */

      opacity:  0;
      transition: opacity  0.3s;
  }

  .tooltip:hover .tooltiptext {
      visibility: visible;
      opacity:  1;
  }
</style>
