// --- Настройки Лотов ---
byte h = 93; // Высота слота
byte slots = 2; // Кол-во Слотов
// --- Настройки Наклеек ---
var lotLeft = Point.get(1009,354); // Верхний Левый угол
var lotRight = Point.get(1041,385); // Правый Нижний угол
// ----- Конфигурация точек -----
var CVET = Point.get(1148,371);          // Основной цвет проверки
var KUPIT = Point.get(1422,361);         // Кнопка "Купить"
var PODTVERDIT = Point.get(749,502);    // Кнопка подтверждения
var NAZAD = Point.get(1478,81);         // Кнопка "Назад"
var OKEY = Point.get(781,492);          // Кнопка "ОК"
var GALOCHKA = Point.get(623,307);      // Кнопка обновления (галочка)
// ----- Настройки цветов -----
var cvetcveta = 17035; // Цвет для проверки цены
var cvetnaz = 6381407;   // Цвет кнопки "Назад"
var cvetgal = 6513492;   // Цвет галочки
var cvetok = 1;    // Цвет кнопки "ОК"
var cvetbuy = 1; // Цвет кнопки "Купить" 
// ----- Настройки скрипта -----
var refreshInterval = 9000;   // Интервал обновления в мс {1000 = 1}

// ----- Ниже не трогать ! ----- 

var lastUpdate = 0;
var skinsFound = 0;
var checksCount = 0;

pfc.startScreenCapture(2);
pfc.log("====================================");
pfc.log(" Скрипт 2в1 успешно запущен!");
pfc.log(" Начинаю мониторинг скинов...");
pfc.log("====================================");

while(!EXIT) 
{
    checksCount++; 
    for(int i = 0; i < slots; i++)
    {
        Point lotLeftC = Point.get(lotLeft.x, lotLeft.y + h * i);
        Point lotRightC = Point.get(lotRight.x, lotRight.y + h * i);
        Point KUPITT = Point.get(KUPIT.x, KUPIT.y + h * i);
        
        if(pfc.getContoursCount(lotLeftC, lotRightC) > 3 && pfc.getColor(KUPIT) == cvetbuy)
        {
            pfc.click(KUPITT);
            pfc.sleep(65);  
            pfc.click(PODTVERDIT);
            pfc.click(PODTVERDIT);
            pfc.sleep(20);
            pfc.click(NAZAD);
            pfc.sleep(15);
            pfc.click(GALOCHKA);             
            pfc.log("====================================");
            pfc.log("Успех! Скин обнаружен в " + Time.getTime());
            pfc.log("Всего найдено скинов: " + (++skinsFound));
            pfc.log("====================================");
        }     
        
        if(pfc.getColor(GALOCHKA) == cvetgal) 
        {
            pfc.click(GALOCHKA);
            pfc.sleep(450);
        }         
           if(pfc.getColor(NAZAD) == cvetnaz)
        {
            pfc.click(NAZAD);
            pfc.sleep(25);
            pfc.click(GALOCHKA);
            pfc.sleep(450);
        }    
        
        if(pfc.getColor(OKEY) == cvetok) 
        {
            pfc.click(OKEY);  
            pfc.sleep(25);
            pfc.click(GALOCHKA);
            pfc.log("Внимание! Перехват в " + Time.getTime());
            pfc.sleep(450);
        }    
        
        if(pfc.getColor(CVET) == cvetcveta && pfc.getColor(KUPIT) == cvetbuy) 
        {  skinsFound++;                
            pfc.click(KUPIT); 
            pfc.sleep(65);  
            pfc.click(PODTVERDIT);
            pfc.click(PODTVERDIT);
            pfc.sleep(20);
            pfc.click(NAZAD);
            pfc.sleep(15);
            pfc.click(GALOCHKA);             
            pfc.log("====================================");
            pfc.log("Успех! Скин обнаружен в " + Time.getTime());
            pfc.log("Всего найдено скинов: " + skinsFound);
            pfc.log("====================================");
            pfc.sleep(450);
        }     
        
        if(Time.getMillis() - lastUpdate >= refreshInterval)
        {
            pfc.click(GALOCHKA);
            pfc.sleep(15);
            pfc.click(GALOCHKA);
            pfc.sleep(100);    
            lastUpdate = Time.getMillis();
        }
    }
}

pfc.log("====================================");
pfc.log(" Скрипт остановлен");
pfc.log(" Итоги работы : " );
pfc.log(" Всего проверок: " + checksCount);
pfc.log(" Найдено скинов: " + skinsFound);
pfc.log("====================================");
