### 0.layout

三种

1. stack pane
2. VBOX
3. HBOX?

但是root 和 scene？不知道区别是啥子哦 无语

### 1. eventhandler lambda expression

实际上是就是反馈，当你click button的时候有东西

```java
public class Main extends Application implements EventHandler{
    Button button;
    @Override
    public void start(Stage primaryStage) throws Exception{
        button  = new Button();
        button.setText("Click me");
        button.setOnAction(e -> System.out.println("aaaaa"));
        StackPane layout = new StackPane();
        layout.getChildren().add(button);
        Parent root = FXMLLoader.load(getClass().getResource("sample.fxml"));
        primaryStage.setTitle("Hello World");
        primaryStage.setScene(new Scene(layout, 300, 275));
        primaryStage.show();
```

![image-20200413175030902](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200413175030902.png)

为什么可以这样用，因为这个接口就只有一个方法哈没错就是这样的，但是为什么用e我就不清楚哈

这里的情况还是跟前面的有所不同 的

然后我试了一下用其他东西也行，终究原因是seton action 其实也只有eventhandle罢了![image-20200413175711840](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200413175711840.png)

所以当大家一对一的时候就可以乱用了

lambda expression 的时候如果想要多个句子的话就直接那个就好了，{}



### 2.直接在scene builder 上操作

其实就相当于setAction中操作了，然后转移到scene builder上面，用一个新建的classok

```java
package sample;

import javafx.event.ActionEvent;
import javafx.fxml.FXML;
import javafx.scene.control.Label;

import java.util.Random;

/**
 * @author zbr
 */
public class MainController {
    @FXML//这个annotation 还是要的
    private Label myMessage;
    public void generateRandom(ActionEvent event){
        Random ran = new Random();
        int myRand  = ran.nextInt(50) + 1;
        myMessage.setText(Integer.toString(myRand));
//        System.out.println(Integer.toString(myRand));
    }
}
```

然后你还可以加点css上去

![image-20200414105912168](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200414105912168.png)

变成这个样子

```css
.button { //这个.的意思代表了全部button
    -fx-font-size: 30px;
    -fx-background-color: rgba(255,255,255,  .80);
    -fx-text-fill: blue;
    -fx-padding: 6 6 6 6;
    -fx-border-radius: 8;
    -fx-font-weight: bold;
}
#myMessage{
    -fx-font-size: 30px;
    -fx-background-color: rgba(255,255,255,  .80);
    -fx-text-fill: blue;
    -fx-padding: 6 6 6 6;
    -fx-border-radius: 8;
    -fx-font-weight: bold;
}

.root{
    -fx-background-color: gray;
}
```



### 3.计算器

```java
public class MainController {
   @FXML
   private Label result;
   private  long number1 = 0;
   private  String operator = "";
   private boolean start = true;
   private Model model= new Model();
   @FXML
   public void processNumbers(ActionEvent event) {
      if (start) {
         result.setText("");
         start = false;
      }
      String value = ((Button) event.getSource()).getText();
      result.setText(result.getText() + value);
   }
   @FXML
   public void processOperators(ActionEvent event){
      String value = ((Button) event.getSource()).getText();

      if(!"=".equals(value)){
         if(!operator.isEmpty()){
            return;
         }
         operator = value;
         number1 = Long.parseLong(result.getText());
         result.setText("");
      }else{
         if(operator.isEmpty()){
            return;
         }
         long number2 = Long.parseLong(result.getText());
         float output = model.calculate(number1,number2,operator);
         result.setText(String.valueOf(output));
         operator = "";
         start = true;
      }
   }
}


public class Model {
    public float calculate(long number1,long number2 , String operator){
       switch (operator){
           case "+":
               return number1 + number2;
           case "-":
               return number1-number2;
           case "*":
               return number1*number2;
           case "/":
               if(number2 == 0){
                   return 0;
               }
               return (float) (1.0*number1/number2);
           default:
               return 0;
       }


    }


}


public class Main extends Application{


    @Override
    public void start(Stage primaryStage) throws Exception{
//        Button button = new Button("Click me");
//        Button exit = new Button("exit");
//        exit.setOnAction(e -> {System.out.println("Exit");
//
//        });
//        button.setOnAction(e -> System.out.println("hello world"));
//        VBox root = new VBox();
//        root.getChildren().addAll(button, exit);
       try {
           Parent root = FXMLLoader.load(getClass().getResource("sample.fxml"));
           Scene scene = new Scene(root, 400, 400);
           scene.getStylesheets().add(getClass().getResource("application.css").toExternalForm());
           primaryStage.setTitle("My title");
           primaryStage.setScene(scene);
           primaryStage.show();
       }
       catch (Exception e){
           e.printStackTrace();
       }


    }


    public static void main(String[] args) {
        launch(args);
    }


}

```





### 4. Combox 

就是选序列的意思嘛，然后呢，有一个observationList

emem反正@FXML 的作用是你可以不直接写在FXML里面，感觉会省空间 而且逻辑会更加清晰说实话

```java
public class MainController implements Initializable {
   @FXML
   public  Label myLabel;
   @FXML
   public ComboBox<String> comboBox;

   ObservableList<String> list = FXCollections.observableArrayList("Mark","Tom","John");

   @Override
   public void initialize(URL location, ResourceBundle resources) {
   comboBox.setItems(list);
   }

   public void comboChanged(ActionEvent event){
      comboBox.getItems().addAll("Ram","Ben","Steve");
      myLabel.setText(comboBox.getValue());
   }
   public void buttonAction(ActionEvent event){
      comboBox.getItems().addAll("Ram","Ben","Steve");
      myLabel.setText(comboBox.getValue());
   }
```

其他的就基本一样了

![image-20200414231703999](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200414231703999.png)

效果图

而且都要initializable 的接口 ememem？？？为啥 上面的comdobox 还有listview 都是哈

![image-20200415003802337](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200415003802337.png)

```java
public class MainController implements Initializable {
   @FXML
   public  Label myLabel;
   @FXML
   public ComboBox<String> comboBox;
   @FXML
   public ListView<String> listView;
   ObservableList<String> list = FXCollections.observableArrayList("Mark","Tom","John");

   @Override
   public void initialize(URL location, ResourceBundle resources) {
   comboBox.setItems(list);
   listView.setItems(list);
   listView.getSelectionModel().setSelectionMode(SelectionMode.MULTIPLE);
   }

   public void comboChanged(ActionEvent event){
      comboBox.getItems().addAll("Ram","Ben","Steve");
      myLabel.setText(comboBox.getValue());
   }
   public void buttonAction(ActionEvent event){
//      listView.getItems().addAll("Ivy", "navin", "Sue");
   }
```

而且用起来也是差不多的