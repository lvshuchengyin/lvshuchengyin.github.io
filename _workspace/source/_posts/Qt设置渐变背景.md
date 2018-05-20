title: Qt设置渐变背景
author: Lscy
tags:
  - qt
categories:
  - 编程
date: 2018-05-20 10:12:00
---
### qss
~~~ css
background-color: qlineargradient(spread:repeat, x1: 0, y1: 0, x2: 0, y2: 1, stop: 0#2ba0d6, stop: 1 #138abd);
~~~

### widget
~~~ cpp
QLinearGradient linearGradient(0, 0, 0, 300);
linearGradient.setColorAt(0.0, Qt::green);
linearGradient.setColorAt(1.0, Qt::blue);
QPalette pal;
pal.setBrush(QPalette::Window, QBrush(linearGradient));
//设置背景自动填充
ui->widget->setAutoFillBackground(true);
ui->widget->setPalette(pal);
~~~