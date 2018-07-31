1.简介
步骤简介
本程序一共分为四个部分
	generate_captcha.py - 利用 Captcha 库生成验证码；
	captcha_model.py - CNN 模型；	
	train_captcha.py - 训练 CNN 模型；
	predict_captcha.py - 识别验证码。
2. 数据学习
安装 captcha 库
	pip install captcha
获取训练数据
generate_captcha.py使用的验证码由数字、大写字母、小写字母组成，每个验证码包含 4 个字符，总共有 62^4 种组合，所以一共有 62^4 种不同的验证码。

理解训练数据
X：一个 mini-batch 的训练数据，其 shape 为 [ batch_size, height, width, 1 ]，batch_size 表示每批次多少个训练数据，height 表示验证码图片的高，width 表示验证码图片的宽，1 表示图片的通道。
Y：X 中每个训练数据属于哪一类验证码，其形状为 [ batch_size, class ] ，对验证码中每个字符进行 One-Hot 编码，所以 class 大小为 4*62。
执行:
获取验证码和对应的分类
获取验证码和对应的分类
python from generate_captcha import generateCaptcha
g = generateCaptcha()
X,Y = g.gen_test_captcha()
查看训练数据
X.shape
Y.shape
可以在目录下查看生成的验证码，jpg格式的图片可以点击查看。
3.模型学习
CNN 模型
captcha_model.py总共 5 层网络，前 3 层为卷积层，第 4、5 层为全连接层。对 4 层隐藏层都进行 dropout。网络结构如下所示： input——>conv——>pool——>dropout——>conv——>pool——>dropout——>conv——>pool——>dropout——>fully connected layer——>dropout——>fully connected layer——>output
然后执行:
python train_captcha.py
使用训练好的模型：
作为实验，可以通过调整 train_captcha.py 文件中 if acc > 0.99: 代码行的准确度节省训练时间(比如将 0.99 为 0.01)，体验训练过程；已经通过长时间的训练得到了一个训练好的模型，可以通过如下命令将训练集下载到本地。
wget http://tensorflow-1253902462.cosgz.myqcloud.com/captcha/capcha_model.zip
unzip -o capcha_model.zip

然后执行:
cd /home/ubuntu;
python train_captcha.py
使用训练好的模型：
作为实验，你可以通过调整 train_captcha.py 文件中 if acc > 0.99: 代码行的准确度节省训练时间(比如将 0.99 为 0.01)，体验训练过程；我们已经通过长时间的训练得到了一个训练好的模型，可以通过如下命令将训练集下载到本地。
wget http://tensorflow-1253902462.cosgz.myqcloud.com/captcha/capcha_model.zip
unzip -o capcha_model.zip
现在可以在 /home/ubuntu 目录下创建源文件 predict_captcha.py，内容可参考：
predict_captcha.py
然后执行:
cd /home/ubuntu;
python predict_captcha.py captcha/0hWn.jpg


