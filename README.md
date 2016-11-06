#ใบงานที่ 3 การตรวจจับ message จากเมาส์และคีย์บอร์ด
##วัตถุประสงค์
1.	เพื่อให้รู้วิธีการเขียนโปรแกรมบน Windows ด้วยฟังก์ชัน Win32 API
2.	เพื่อให้มีความคุ้นเคยกับการใช้เครื่องมือต่างๆ ในการสร้าง Application บน IDE

##ลำดับการทดลอง
1.	สร้าง Project ใหม่ เป็นชนิด  Win32 Project แบบ empty project ตามใบงานที่ 1
2.	เพิ่มไฟล์ .cpp ใหม่ เข้าไปใน Project  
3.	คัดลอกไฟล์ .cpp จากการทดลองที่ 2
4.	แก้ไข code ในส่วนของการ switch (message) ในไฟล์ .cpp ให้เป็นไปดังต่อไปนี้
5. กดปุ่ม F5 เพื่อดูผลการทำงานของโปรแกรม
 
```c
    switch (message) {

    case WM_PAINT:
        hdc = BeginPaint (hwnd, &ps);
//      Ellipse (hdc, 10, 10, 200, 100);
        EndPaint (hwnd, &ps);
        return 0;

    case WM_LBUTTONDOWN:
        char str[256];
        POINT pt;   // point of mouse clicked, received via message
        pt.x = LOWORD(lParam);
        pt.y = HIWORD(lParam);
        wsprintf(str,"WM_LBUTTONDOWN\nCo-ordinate are\n (%i, %i)",pt.x,
                     pt.y);
        MessageBox(hwnd, str, "Left Button Clicked", MB_OK);
        return 0;

    case WM_RBUTTONDOWN:
        pt.x = LOWORD(lParam);
        pt.y = HIWORD(lParam);
        wsprintf(str,"WM_RBUTTONDOWN\nCo-ordinate are\n (%i, %i)",pt.x,
                     pt.y);
        MessageBox(hwnd, str, "Right Button Clicked", MB_OK);
        return 0;

    case WM_CHAR:
        hdc = GetDC(hwnd);
        TextOut(hdc, 1,1, "  ",3);
        wsprintf(str,"%c",(char) wParam);
        TextOut(hdc, 1,1, str,strlen(str));
        ReleaseDC(hwnd, hdc);
        return 0;

    case WM_DESTROY:
        PostQuitMessage (0);
        return 0;
    }
```

##คำถาม 

1.	นักศึกษาพบปัญหาในการคอมไพล์โปรแกรมหรือไม่ ถ้าเจอให้บอกที่ผิดและแนวทางการแก้ไข

  เหมือนกับใบงานที่สองคือคอมไพล์ไม่ผ่านเนื่องจาก } ไม่ครบ แก้ไขโดยใส่เพิ่มไป 1 ตัว } จะทำให้การคอมไพล์ผ่านได้
  
 
