### Airflow nedir?
- Airflow; taskları doğru zamanda, doğru sırayla ve doğru bir şekilde çalıştırmayı sağlayan bir orkestrasyon aracıdır.
- Airflow 2014 yilinda Airbnb tarafindan gelistirildi.
- Compleks is akislarini workflowlar yonetmek icin kullanilir
- Python ile yazilmis

### Workflow nedir
- Gorevler(Taskler) dizisidir.
- Bu dizilere DAG(directed acylic graph) diyoruz airflowda
- Ornegin A taski bittiginda B ve C taskleri baslatilir. Bunlar bittginde D ve E tasklari baslatilir. D bittiginde tekrar A taskinin baslatilmasina izin vermez. C taskindan sonra da A'ya donemez. Bu yuzden dag taskler dizisidir. Bir yolda ilerlemesi istenir. iliski ve dependencieleri vardir.
- Gecmiste baslatilan bir DAG varsayilan olarak gunumuze kadar otomatik gelir. Bunu bir tane environment variable ile degistirmek mumkun

### Task nedir?
- her bir gorevdir. dag icindeki A, B, C, D ve E gibi.
- Taskler Python ile yazilir.
- Taskler arasinda bagimliliklar olabilir.
- taskler spesifik bir isin yapilmasini amaclar. Kullanilan methoda ise operator denir. 
- bircok operator vardir.

### Operator tipleri
- BashOperator
- PythonOperator
- ...
- Customized operator
- Kendi operatorunu yazmak da mumkun
- pythonoperator bir python code'u calistirir.

### Operator vs Task
- operator ne yapilacagini belirler
- task ise operatorun yapacagi isi uygular
- dag ise tasklerin birlesimidir.
- bir taskin icinde birden fazla operator olabilir.

### Execution Date
- Dag'in calsitirildigi tarih ve saattir.

### Task Instance
- Execution Date'te belirtilen taskin calistirilmasidir.

### Dag Run
- Execution Date'te belirtilenDag calistirilmasidir.

### Task Lifecycle
- 11 tanedir. 
- airflow webserverda gorebiliriz bunlari. tree views ya da graphta
- no_status, scheduled, queued, running success, upstream_failed, up_for_reschedule, skipped, up_for_retry, failed, shutdown
- scheduler tarafinda - scheduled, removed, upstream failed, skipped
- eger scheduled olduysa executera task verilir. Queued yani siraya alinir. worker'a verilir ve runninge gecer. runningteki sonuc success, failed ya da kendimizin durdurdugu shutdown olabilir. eger hata verdiyse yani failed olduysa belirttigimiz sayida tekrara girer. Bu status da Up for retry"dir.
- Bazi durumlarda runninge geldiginde Up for schedule edilerek tekrar task Schedulera gonderilir. Ornegin S3 kaydedilmis bir dosya bekliyorsak bununun use case'dir.
- Web server, scheduler, executer ve workers database'e baglidir. haberlesir. durumlarini bildirir.

### ETL - Extract Transform Load
-  verinin bir kaynaktan alınıp belirli işlemlerden geçirildikten sonra hedefe kaydedilmesi işlemlerine ETL(Extract Transform Load) denir.

### Ozellikleri

Dinamik: Python ile ne yapılabiliyorsa airflow ile de yapılabiliyor bu da tasklarımızı oluştururken muazzam bir dinamiklik sağlıyor.

Ölçeklendirilebilir: İstenilen kadar task kolayca paralel çalıştırılabiliyor.

Kullanıcı Arayüzü: Kullanışlı bir UI’a sahip. Data pipelinelarda oluşan hatalar ve nerede oluştuğu kolayca gözlemlenebiliyor. Hata alan tasklar yeniden başlatlabiliyor.

Genişletilebilir: Yeni bir araç çıktığında Airflow’un güncellenmesini beklemek gerekmiyor. Kendi eklentilerinizi yazıp kolayca entegre edebiliyorsunuz.

### Bilesenler

Web Server: Flask sunucusu UI’ı serve ediyor. Airflow'un kullanıcı arayüzünü sağlar. Görevlerin durumunu izlemek, iş akışlarını başlatmak, duraklatmak veya yeniden başlatmak, görev geçmişini görüntülemek ve yapılandırma ayarlarını yönetmek gibi işlemleri gerçekleştirmenizi sağlar.

Scheduler: Workflowları schecudle eden deamon. Airflow’un en önemli componentidir.

Metastore: Metadata’nın saklandığı veritabanı. Airflow'un durum ve yapılandırma bilgilerini sakladığı veritabanıdır. Görevlerin durumu, bağımlılıklar, iş akışı tanımları, zamanlama bilgileri ve daha fazlası gibi bilgileri tutar. Airflow, SQLite, MySQL, PostgreSQL veya başka bir desteklenen veritabanı kullanabilir.

Executor: Taskların nasıl çalışması gerektiğinin tanımlandığı sınıf. Görevleri gerçekleştirmek için kullanılan işçi süreçleridir. Airflow, farklı executor tiplerini destekler, örneğin LocalExecutor, CeleryExecutor veya KubernetesExecutor gibi.

Worker: Taskı execute eden process veya sub proccess. Scheduler, görevleri işçi süreçlere dağıtmak ve durumlarını takip etmek için bir mesajlaşma kuyruğu sistemine ihtiyaç duyar. Airflow, mesajlaşma kuyruğu olarak RabbitMQ, Redis, Apache Kafka gibi sistemleri destekler.

### DAG (Directed Acyclic Graph)
DAG Airflow’un temel konseptidir. Taskları, bağımlılık ve ilişkileri ile bir araya getirip nasıl çalışmalarını söyler.

### Operator
- Operator taskı kapsayan bir wrapperdır. Varsayılan olarak farklı tipte birçok operator bulunur.

Action Operators: Fonksyionları veya komutları execute ettiğimiz operatorler örn: bash scriptleri, python kodu

Transfer Operators: Kaynaktan hedefe veri taşımaya yarayan operatorler örn: ElasticSearch to Mysql

Sensor Operators: Başka bir işleme geçmeden önce bir şeyin olmasını beklemek için kullanılan operatorler örn: bir dizinde dosya var mı diye bekleyip, varsa diğer taska geçmek.

### export AIRFLOW_HOME = .
- airflowa calistigi folderin neresi oldugunu gosterir.

### airflow db init
- sqlite database olusturur,
- log olusturur.
- bayi configuration dosyasi olusturur.

### airflow webserver -p 8080
- 8080 portunda flask ile airflow web servisini acar.

### airflow users create --help
- komut hakkinda bilgiler verir.

### airflow users create --username admin --firstname sahin --lastname erdo --role Admin --email admin@domain.com
- user olusturma
- admin user

### airflow scheduler
- scheduleri calistirir.

### Postgresoperator
- bu poerator ile browserden connection ayarlarini yaptigimiz postgresqle komut gondermek mumkun.
- SQL komutlarla yapilir bu.

### Airflow icinde python modulleri ekleme
- iki yolu var.
- birincisi base airflow image ile requirements.txt dosyasini ekleyip yuklemek
- ikincisi airflow source kodlarin icindeki docker-context-files icinde requirements.txt dosyasi olusturup source kodtan bir yeni image olusturmak.

### Sensor Operator
- birseyin olmasi icin bekleyen operator
- ozellikle bir dosyanin ne zaman olusacagini bilmedigimiz durumlar icin cok kullanisli
- poking kavrami: kontrol edilen dosya ornegin ordaysa hemen sonucu gosterir ama eger orda yoksa belli araliklarla check eder.
- mode poke, poke_intervals ve timeout degerleri verilir. kac saniyede bir kontrl edilecegi ve toplamda ne kadar sure anlamalrina gelir sirayla.

### Dokumantasyondaki macrolarda
- airflowda bulunan environment variable bilgileri ve iceriklerinin ne oldugu var.

### Hooklar
- database, yada bir bulut servisiyle connection kurmak icin ya da birseyer gonderip almak icin kullanilabilir.

### airflow dag list
- dagleri listeler

### dag_dir_list_interval
- eklenen dagin browsera gelmesi icin gereken sure.