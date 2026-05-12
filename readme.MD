# Publisher Reflection

### How much data your publisher program will send to the message broker in one run?
Dalam satu kali run, program publisher mengirimkan lima data atau lima event ke message broker. Kelima event tersebut adalah data `UserCreatedEventMessage` dengan `user_id` dari 1 sampai 5 dan `user_name` yang berbeda-beda, yaitu Amir, Budi, Cica, Dira, dan Emir. Setiap data dikirim menggunakan fungsi `publish_event` dengan routing atau nama event yang sama, yaitu `user_created`. Artinya, setiap kali program publisher dijalankan, publisher akan membuat lima pesan lalu mengirimkannya ke RabbitMQ sebagai message broker. Setelah pesan masuk ke RabbitMQ, pesan tersebut dapat diterima dan diproses oleh subscriber yang sedang mendengarkan queue atau event `user_created`. Mekanisme ini menunjukkan bahwa publisher tidak berkomunikasi langsung dengan subscriber, tetapi melalui perantara message broker.

### The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?
URL `amqp://guest:guest@localhost:5672` pada publisher sama dengan URL yang digunakan pada subscriber. Hal ini berarti publisher dan subscriber terhubung ke message broker yang sama, yaitu RabbitMQ yang berjalan di komputer lokal. Kata `guest` pertama adalah username untuk mengakses RabbitMQ, sedangkan `guest` kedua adalah password dari username tersebut. Bagian `localhost` menunjukkan bahwa RabbitMQ berjalan pada komputer yang sama dengan program publisher dan subscriber. Angka `5672` adalah port default yang digunakan RabbitMQ untuk koneksi AMQP. Karena publisher dan subscriber memakai URL yang sama, maka event yang dikirim oleh publisher dapat masuk ke RabbitMQ yang sama dan kemudian diterima oleh subscriber yang sesuai.

# Screenshot RABBITMQ

![Rabbit mq](static/Rabbit.PNG)

Subscriber connnected
![Rabbit sub](static/RabbitSub.PNG)

Subscriber console
![Rabbit pub](static/RabbitPub2.PNG)
![Rabbit pub](static/RabbitPub.PNG)

Pada tahap ini, subscriber dijalankan terlebih dahulu agar siap menerima event dari message broker. Setelah itu, publisher dijalankan menggunakan perintah `cargo run`. Dalam satu kali eksekusi, publisher mengirimkan lima event `UserCreatedEventMessage` ke RabbitMQ melalui event bernama `user_created`. Kelima event tersebut berisi data pengguna dengan `user_id` dan `user_name`, seperti Amir, Budi, Cica, Dira, dan Emir. Setelah event masuk ke RabbitMQ, subscriber yang sedang mendengarkan queue tersebut menerima dan memproses pesan satu per satu. Hal ini terlihat dari terminal subscriber yang menampilkan output `Message received` untuk setiap event yang dikirim oleh publisher. Dengan demikian, proses ini menunjukkan bahwa publisher dan subscriber tidak berkomunikasi secara langsung, tetapi melalui RabbitMQ sebagai message broker. Menurut saya, mekanisme ini membuat sistem lebih fleksibel karena publisher tetap dapat mengirim event tanpa harus menunggu subscriber memprosesnya secara langsung.
