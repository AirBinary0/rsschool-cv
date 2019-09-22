# Resume for "Junior JS developer" position
## Base information about me
1. My name is Dzmitry Kim. I am 26 age old. I am from Belarus and now I am live in Minsk.
2. If you want contact with me, use one or more ways below:
    1. **Mobile phone:** +375-29-355-90-27 (Velcom/A1);
    2. **Mobile phone, Viber, Telegram:** +375-33-632-57-92 (MTS);
    3. **E-mails:** d.kim2009@tut.by, d.kim2009k@gmail.com;
    4. **Skype:** *reduserdemon*;
    5. **Discord:** DmitryKim#0080.
3. **Summary.** At now I work in National Academy of Science of Belarus on engineer-programmer position. I have some experience in desktop and web development. I made some interfaces and some features for [ANALYSIS OF RELIABILITY 
AND SURVIVABILITY OF ON-BOARD EQUIPMENT OF SMALL SATELLITES](https://journals.ssau.ru/index.php/vestnik/article/view/5624). Also I made some desktop programs used C++ Qt. At now I make blockchain network and chaincode based on Hyperledger Fabric and node JS. I sure after the course i can use JS better and more efficient and I can made more beautiful sites. The course is good experience for me to get best practices and also show my skills and my well ability to study new things.
## Skills @ Code Examples
4. **Skills**
    1. Programming languages:
        1. C++ / *It's my main language;*
        2. HTML+CSS+JS / *The second stack that I use;*
        3. C#, Java / *A little bit.*
    2. Frameworks:
        1. C++ Qt;
        2. JQuery, Ajax, CanvasXpress.
    3. Git control version system
5. **Code examples:**
    1. C++ Qt code example:
    ```cpp
    void Scatter3D::parseData()
    {
        container->setVisible(false);
        loadProgress->setMaximum(file.count()*2);
        loadProgress->setValue(1);
        loadProgress->setVisible(true);
        label->setVisible(true);
        //----- file edit -----
        while (file.last()=="")
            file.removeLast();
        //----- end file edit -----
        removeAllSeries();

        //----- Get cluster count -----
        int max_number = 0;
        cluster_items_count.clear();
        maxCol = file[0].split('\t').count()-1;
        emit setSpin(8,2,maxCol,firstCol);
        emit setSpin(9,2,maxCol,secondCol);
        emit setSpin(10,2,maxCol,thirdCol);
        for (int i=0; i<file.count(); i++)
        {
            int mark = file[i].split('\t')[1].toInt();
            if (mark >= max_number)
            {
                max_number = mark;
                while (cluster_items_count.length()<=max_number)
                {
                    cluster_items_count.append(0);
                }
            }
            loadProgress->setValue(loadProgress->value()+1);
            cluster_items_count.replace(mark,cluster_items_count.at(mark)+1);
        }
        cluster_count = max_number+1;
        //----- End cluster count -----

        //----- Configure axes headers -----
        graph->axisX()->setTitle("X");
        graph->axisY()->setTitle("Y");
        graph->axisZ()->setTitle("Z");

        for (int i=0; i<cluster_count; i++)
        {
            QScatterDataProxy *proxy = new QScatterDataProxy;
            QScatter3DSeries *series = new QScatter3DSeries(proxy);
            series->setName(QStringLiteral("Кластер # %1").arg(i));
            series->setItemLabelFormat(QStringLiteral("@seriesName. @xTitle: @xLabel @yTitle: @yLabel @zTitle: @zLabel"));
            series->setMeshSmooth(true);
            graph->addSeries(series);
            QScatterDataArray *dataArray = new QScatterDataArray;
            dataArray->resize(cluster_items_count.at(i)!=0?cluster_items_count.at(i):1);
            allClusterDataArrays.append(dataArray);
            QScatterDataItem * ptrToDataArray = &dataArray->first();
            allPointersToDataArray.append(ptrToDataArray);
        }

        //----- Insert data -----
        QStringList pieces;
        for (int i=0; i<file.count(); i++)
        {
            pieces = file[i].split('\t');
            int mark = pieces[1].toInt();
            QScatterDataItem *ptrToDataArray = allPointersToDataArray.at(mark);
            ptrToDataArray->setPosition(QVector3D(pieces[firstCol].toDouble(),
                                                pieces[secondCol].toDouble(),
                                                pieces[thirdCol].toDouble()));
            allPointersToDataArray.replace(mark,ptrToDataArray+1);
            loadProgress->setValue(loadProgress->value()+1);
            //if (i=0)
        }
        //----- End insert data
        for (int i=0; i<cluster_count; i++)
        {
            graph->seriesList().at(i)->dataProxy()->resetArray(allClusterDataArrays.at(i));
        }
        loadProgress->setVisible(false);
        label->setVisible(false);
        container->setVisible(true);
        this->setFocus();
        connect(graph,SIGNAL(activeChanged()),this,SLOT(setWindowFocus()));
    }
    ```
    2. js code example:
    ```javascript
    function repaintFeatureAll(){
        canvasZero = null;
        $('#graphFrame').html('<div id="json_view"></div><canvas class="canvas0" id="canvas0">');
        rtr();
        document.getElementById('preloader').style.display = 'block';
        var gen =  $('#inp3Tool').val();
        var dataCan = new Object();
            var ann = [];
        dataCan.x = {};
        for (i=popSize*(gen-1); i<popSize*gen;i++){
            ann.push(i);
        }
        dataCan.x.Species = ann;
        dataCan.y = {};
            ann = [];
        for(var i=0; i<dataFirst[0].length; i++){
            ann.push('K'+i);
        }
        dataCan.y.vars = ann;

        ann = [];
        for (var i=popSize*(gen-1); i<popSize*gen; i++){
            ann.push(i);
        }
        dataCan.y.smps = ann;
        ann = [];
        for (var i=0; i<dataFirst[0].length; i++) {
            setD = [];
            for (var j=popSize*(gen-1); j<popSize*gen; j++){
                setD.push(dataFirst[j][i]);
            }
            ann.push(setD);
        }
        dataCan.y.data = ann;
        console.log(dataFirst);
        var conf = {"axisAlgorithm": "wilkinson",
                    "axisMinMaxTickTickWidth": false,
                    "codeType": "pretty",
                    "graphOrientation": "vertical",
                    "missingDataValue": "NA",
                    "smpDendrogramNewick": false,
                    "summaryType": "raw",
                    "title": "Вся популяция (gen "+$('#inp3Tool').val()+")",
                    "varDendrogramNewick": false,
                    "smpLabelRotate": 90,
                    "xAxis": [
                        "Важность"
                    ],
                    "xAxisTitle": "Важность"};
        showCanvas(dataCan,conf,0); 
        document.getElementById('preloader').style.display = 'none';
        document.getElementById('statusDiv').innerHTML = '<div class="statusText">'+'FSGUI'+'</div><div class="statusSeparator">|</div><div class="statusText">'+'Вся популяция'+'</div><div class="statusSeparator">|</div><div class="statusText">'+'Генерация '+$('#inp3Tool').val()+' из '+maxStep+'</div>';
    }
    ```
## Experience & Education
6. **Experience.** I have some experience in desktop and web development. I made some interfaces and some features for [ANALYSIS OF RELIABILITY 
AND SURVIVABILITY OF ON-BOARD EQUIPMENT OF SMALL SATELLITES](https://journals.ssau.ru/index.php/vestnik/article/view/5624). Also I made some desktop programs used C++ Qt. At now I make blockchain network and chaincode based on Hyperledger Fabric and node JS. 
7. **Education.** From 2010 to 2015 years I studied in Belarus National Technique University on cathedra Intelligent systems. From 2017 to 2019 years I studied at magistracy.
8. **English.** I have **Elementary** English level (A2) after Elementary course of Streamline English school. Now I study Pre-intermediate (A2+) course in Streamline English school. 