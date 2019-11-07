# ApacheSuperset
Centos7 Apache Superset install.

Sanal makina olarak kurulan Centos7 kurulumu tamamlandıktan sonra veri görselleştirme için kullanılacak Apache Superset servisi kurulumu
aşağıdaki adımlardan oluşmaktadır.

Öncelikle python'u güncelleştirmemiz gerekecek. Aşağıdaki komutlardan birisi iş görecektir.

sudo yum upgrade python-setuptools
 
veya
 
yum upgrade python-setuptools

ardından aşağıdaki kurulum ile işleme devam edilir,

sudo yum install gcc gcc-c++ libffi-devel python-devel python-pip python-wheel openssl-devel libsasl2-devel openldap-devel

veya

yum install gcc gcc-c++ libffi-devel python-devel python-pip python-wheel openssl-devel libsasl2-devel openldap-devel

Bu işlemler tamamlandıktan sonra python default olarak 2.7 olarak kurulmuş olacaktır. Superset servisi artık 2.+ servisler için 
support yapmadığı için 3.+ versiyonlar kurulması gerekiyor ve değiştirilmesi gerekiyor bu işlemler için şu adımlar takip edilir.

yum install centos-release-scl

veya 

sudo yum install centos-release-scl

SCL Python 2.7 sürümünü 3.+ sürümüne yükseltmek için gerekli olan araçtır.

Python kurulumu gerçekleştirilir.

yum install rh-python36

veya

sudo yum install rh-python36

bir önceki adımda kurulan SCL ile birlikte aşağıdaki komut satırı ile birlikte değiştirme işlemi gerçekleştirilir.

scl enable rh-python36 bash

Artık python sürümümüz 3.6 olarak ayarlanmıştır.

Python içerisinde kullanılacak kütüphaneleri yükleyebilmemize yarayan pip'i en son sürümüne güncelleştiririz. 

pip install --upgrade setuptools pip

ve 

curl "https://boostrap.pypa.io/get-pip.py" -o "get-pip.py" adresinden indirilen dosya get-pip.py adı ile curl sayesinde değiştirilir.

Python ile açılarak içerisinde bulunan güncelleştirmeler yapılmış olunur. Aşağıda yapılacak işlem tanımlanmıştır.

python get-pip.py

Bu işlemin ardından SUPERSET kurulumlarına başlayabiliriz.

öncelikle;

pip install superset kurulur.

superset db upgrade ile database initial haline getirilir.

Kurulacak olan port üzerinden Superset arayüzüne giriş yapabilmek için gerekli olan kullanıcı adı ve şifre işlemleri Flask sayesinde
aşağıdaki komut satırı ile birlikte yapılır.

flash fab create-admin 

komut satırı yazıldıktan sonra kullanıcı adı, ad, soyad, email, şifre ve re-şifre girilerek işlemlere devam edilebilir.

superset load_examples işlemi ile birlikte bazı datalar yüklenir.

superset init komut satırı ile birlikte hazır roller ve izinler verilir.

en son olarak yapacağımız işlemde port açılarak arayüze giriş yapılabilir. 

superset run -h 10.254.183.28 -p 8080 --with-threads --reload --debugger

yapılarak localhost:8080/ portuna girilebilir.

Firewall servislerini devre dışı bırakmamız gerecektir bu yüzden 

service firewalld stop komut satırı yazılır.
