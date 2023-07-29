Murphy, Sean smurphy at walbro.com
Wed Jun 4 17:14:43 CEST 2014
Previous message: [Qt-creator] Load OTHER_FILES with Qt-Creator 3.1.1
Next message: [Qt-creator] Help debugging a heap error
Messages sorted by: [ date ] [ thread ] [ subject ] [ author ]
I've recently introduced a bug in my program that is causing my application to crash when quitting, but I'm having trouble figuring out what is causing it.  The error reported in the Application Output window is:
  HEAP: Free Heap block 15b73e68 modified at 15b73e80 after it was freed

Here's the debugger stack
0              ntdll!TpWaitForAlpcCompletion                C:\windows\system32\ntdll.dll                 0x77410575
1              ??                                           0x28f5c8
2              ntdll!AlpcMaxAllowedMessageLength   C:\windows\system32\ntdll.dll                 0x773ca412
3              ??                                           0x15b73e68
4              ntdll!RtlReleasePebLock               C:\windows\system32\ntdll.dll                 0x773735b7
5              ??                                           0xd
6              ??                                           0x8
7              ??                                           0x28f690
8              ntdll!LdrLoadAlternateResourceModuleEx          C:\windows\system32\ntdll.dll                 0x773734a2
9              ??                                           0x15b73ed0
10           ntdll!RtlValidateHeap     C:\windows\system32\ntdll.dll                 0x7741172e
11           ??                                           0x13e50000
12           ntdll!AlpcMaxAllowedMessageLength   C:\windows\system32\ntdll.dll                 0x773cac29
13           ??                                           0x13e50000
14           ntdll!LdrLoadAlternateResourceModuleEx          C:\windows\system32\ntdll.dll                 0x773734a2
15           ??                                           0x15b73ed0
16           msvcrt!free        C:\windows\syswow64\msvcrt.dll                           0x75e798cd
17           ??                                           0x13e50000
18           QtSharedPointer::ExternalRefCountData::operator delete           qsharedpointer_impl.h 168         0x6b9bed05
19           QObject::~QObject         qobject.cpp        796         0x6b9401b4
20           QAction::~QAction          qaction.cpp        576         0xa602c45
21           QAction::~QAction          qaction.cpp        600         0xa602c73
22           QObjectPrivate::deleteChildren                qobject.cpp        1835       0x6b941c3f
23           QWidget::~QWidget       qwidget.cpp       1486       0xa62ec02
24           QMainWindow::~QMainWindow             qmainwindow.cpp          378         0xa7547fe
25           MainWindow::~MainWindow    mainwindow.cpp             249         0x4059d1
26           qMain   main.cpp             8              0x40168e
27           WinMain at 16     qtmain_win.cpp               131         0x43a2ed
28           main                                      0x469a4d

I've set a breakpoint in my MainWindow ::~MainWindow(), but I'm able to successfully step through all of my code without anything crashing.  I'm pretty weak at using debuggers, so I'm unsure what to try next?

As you can see from the stack trace, I'm on Windows.  And I'm not sure what other tools I have at my disposal to help out?
Sean
-------------- next part --------------
An HTML attachment was scrubbed...
URL: <http://lists.qt-project.org/pipermail/qt-creator/attachments/20140604/673de6f9/attachment.html>
Previous message: [Qt-creator] Load OTHER_FILES with Qt-Creator 3.1.1
Next message: [Qt-creator] Help debugging a heap error
Messages sorted by: [ date ] [ thread ] [ subject ] [ author ]
More information about the Qt-creator mailing list
