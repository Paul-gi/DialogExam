# DialogExam
有多選是 單選是 多健式 沒有做進度條型
java
-------------------------------------------------------------------------------------
package com.sinopac.dialogexam;

import android.app.AlertDialog;
import android.content.DialogInterface;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        //---1
        Button btn = (Button)findViewById(R.id.getBtn);
        //---2
        Button btn_two = (Button)findViewById(R.id.getBtn_Two);
        //---3
        Button btn_three = (Button)findViewById(R.id.getBtn_Three);
        final String[] colors = { "Pink", "Red", "Yellow", "Blue" };
        final ArrayList<Integer> slist = new ArrayList();
        final boolean icount[] = new boolean[colors.length];
        final String[] msg = {""};

        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                AlertDialog.Builder builder = new AlertDialog.Builder(MainActivity.this);
                builder.setTitle("Login Alert")
                        .setMessage("Are you sure, you want to continue ?")
                        .setIcon(R.drawable.dialog_icon)
                        .setCancelable(false);
                    //在這裡加入一個edittext
                        final  EditText et = new EditText(MainActivity.this);
                        builder.setView(et);
                    //這邊的setPosition如果不需要edit可以把bulider拿掉把ET取消
                        builder.setPositiveButton("Yes", new DialogInterface.OnClickListener() {
                            @Override
                            public void onClick(DialogInterface dialog, int which) {
                               // Toast.makeText(MainActivity.this,"Selected Option: YES",Toast.LENGTH_SHORT).show();
                                String message ="";
                                message +=et.getText();
                                Toast.makeText(MainActivity.this,message,Toast.LENGTH_SHORT).show();
                            }
                        })
                        .setNegativeButton("No", new DialogInterface.OnClickListener() {
                            @Override
                            public void onClick(DialogInterface dialog, int which) {
                                Toast.makeText(MainActivity.this,"Selected Option: No",Toast.LENGTH_SHORT).show();
                            }
                        })
                        .setNeutralButton("沒意見",new DialogInterface.OnClickListener(){
                            @Override public void onClick(DialogInterface dialog, int which) {
                                dialog.dismiss();
                            }
                        });
                //特殊的可以加入if else做出現的判斷
                        /*.setPositiveButton("Yes", new DialogInterface.OnClickListener() {
                            @Override
                            public void onClick(DialogInterface dialog, int which) {
                                Toast.makeText(MainActivity.this,"Selected Option: YES",Toast.LENGTH_SHORT).show();
                            }
                        })*/

                //Creating dialog box
                AlertDialog dialog  = builder.create();
                dialog.show();
            }
        });

                                //2
        btn_two.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                AlertDialog.Builder builder = new AlertDialog.Builder(MainActivity.this);
                builder.setTitle("Choose Colors")
                        .setMultiChoiceItems(colors,icount, new DialogInterface.OnMultiChoiceClickListener() {
                            @Override
                            public void onClick(DialogInterface arg0, int arg1, boolean arg2) {
                                if (arg2) {
                                    // If user select a item then add it in selected items
                                    slist.add(arg1);
                                } else if (slist.contains(arg1)) {
                                    // if the item is already selected then remove it
                                    slist.remove(Integer.valueOf(arg1));
                                }
                            }
                        })      .setCancelable(false)
                        .setPositiveButton("Yes", new DialogInterface.OnClickListener() {
                            @Override
                            public void onClick(DialogInterface dialog, int which) {
                                msg[0] = "";
                                for (int i = 0; i < slist.size(); i++) {
                                    msg[0] = msg[0] + "\n" + (i + 1) + " : " + colors[slist.get(i)];
                                }
                                //這樣比較正確 因為有一點生命週期的問題
                                //Toast.makeText(MainActivity.this, "Total " + slist.size() + " Items Selected.\n" + msg[0], Toast.LENGTH_SHORT).show();
                                Toast.makeText(getApplicationContext(), "Total " + slist.size() + " Items Selected.\n" + msg[0], Toast.LENGTH_SHORT).show();
                            }
                        })
                        .setNegativeButton("No", new DialogInterface.OnClickListener() {
                            @Override
                            public void onClick(DialogInterface dialog, int which) {
                                Toast.makeText(MainActivity.this,"No Option Selected",Toast.LENGTH_SHORT).show();
                            }
                        });
                //Creating dialog box
                AlertDialog dialog  = builder.create();
                dialog.show();
            }
        });

                                    //3
        btn_three.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                AlertDialog.Builder builder = new AlertDialog.Builder(MainActivity.this);
                builder.setTitle("Choose single")
                       .setIcon(R.drawable.dialog_icon);
                builder.setSingleChoiceItems(colors,0, new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        List<String> list = Arrays.asList((colors));
                        Toast.makeText(MainActivity.this,list.get(which),Toast.LENGTH_SHORT).show();
                        dialog.dismiss();
                    }
                });
                        builder.setNegativeButton("cancel", new DialogInterface.OnClickListener() {
                            @Override
                            public void onClick(DialogInterface dialog, int which) {
                                Toast.makeText(MainActivity.this,"No Option Selected",Toast.LENGTH_SHORT).show();
                            }
                        });
                //Creating dialog box
                AlertDialog dialog  = builder.create();
                dialog.show();
            }
        });
    }
    }
----------------------------------------------------------------------------------------------------------------------
  XML
--------------------------------------------------------------------------------------------------------------------
  <?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/getBtn"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="92dp"
        android:text="是與否和文字輸入與icon"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/getBtn_Two"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="56dp"
        android:text="多選"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/getBtn" />

    <Button
        android:id="@+id/getBtn_Three"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="64dp"
        android:text="單選"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/getBtn_Two" />

</androidx.constraintlayout.widget.ConstraintLayout>
