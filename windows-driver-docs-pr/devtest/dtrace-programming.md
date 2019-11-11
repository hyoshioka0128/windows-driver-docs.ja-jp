---
title: DTrace プログラミング
description: DTrace は、D プログラミング言語をサポートしています。 このトピックでは、D コードサンプルについて説明します。
ms.assetid: abf23d76-423d-4d1e-afde-83739015bbff
keywords:
- DTrace WDK
- ソフトウェアトレース WDK、DTrace
- トレースメッセージの表示
- トレースメッセージの書式設定 WDK DTrace
- トレースメッセージの書式設定 WDK DTrace
- ソフトウェアトレース WDK, 書式設定メッセージ
- WDK のトレース、DTrace
- トレースメッセージフォーマットファイル WDK
ms.date: 11/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8a7be2b6213155587c166a1b96d950b7c20c4fcf
ms.sourcegitcommit: 5081de283b09b4fe847912fc1dc0e7f057e0a0cd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73592433"
---
# <a name="dtrace-programming"></a>DTrace プログラミング

DTrace は、D プログラミング言語をサポートしています。 このトピックでは、DTrace スクリプトの記述と使用を開始する方法について説明します。

Windows 上の DTrace に関する一般的な情報については、「 [dtrace](dtrace.md)」を参照してください。

DTrace の詳細については、ケンブリッジの大学の[OpenDTrace 仕様バージョン 1.0](https://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-924.pdf)を参照してください。

> [!NOTE]
> DTrace は、バージョン18980および Windows Server Insider Preview ビルド18975以降の Windows の Insider ビルドでサポートされています。

## <a name="additional-sample-scripts"></a>その他のサンプルスクリプト

Windows のシナリオに適用される追加の D スクリプトは、DTrace ソースコードの samples ディレクトリにあります。

[https://github.com/microsoft/DTrace-on-Windows/tree/master/samples/windows](https://github.com/microsoft/DTrace-on-Windows/tree/master/samples/windows)

Opentrace toolkit スクリプトのセットは、 [https://github.com/opendtrace/toolkit](https://github.com/opendtrace/toolkit)で入手できます。


## <a name="hello-world"></a>Hello World

DTrace スクリプトは、コマンドおよび D プログラミングスクリプト要素を含む単純なテキストファイルです。

```dtrace
dtrace:::BEGIN
{
  trace("Hello World from DTrace!");
  exit(0);
}
```

ファイルを helloworld として保存します。

管理者としてコマンドプロンプトウィンドウを開き、-s オプションを使用してスクリプトを実行します。

```dtrace
dtrace -s helloworld.d
dtrace: script '.\helloworld.d' matched 1 probe
CPU     ID                    FUNCTION:NAME
  0      1                           :BEGIN   Hello World from DTrace!
```

## <a name="ntcreateuserprocess-return-time"></a>NtCreateUserProcess の戻り時間

DTrace スクリプトを作成して、複数の関数/イベント間でかかった時間を追跡することができます。 次に示すのは、作成プロセスの entry/return 間で NtCreateUserProcess 関数を追跡する単純な例です。

```dtrace

syscall::NtCreateUserProcess:entry
{
    self->ts = timestamp;
}

syscall::NtCreateUserProcess:return
{
    printf(" [Caller %s]: Time taken to return from create process is %d MicroSecond \n", execname, (timestamp - self->ts)/ 1000);
}

```

ファイルを ntcreatetime. d として保存し、-s オプションを使用してテストスクリプトを実行します。


```dtrace
C:\Windows\system32>dtrace -s ntcreatetime.d
dtrace: script 'ntcreatetime.d' matched 2 probes
CPU     ID                    FUNCTION:NAME
  0    183       NtCreateUserProcess:return  [Caller svchost.exe]: Time taken to return from create process is 51191 MicroSecond

  0    183       NtCreateUserProcess:return  [Caller SearchIndexer.]: Time taken to return from create process is 84418 MicroSecond

  0    183       NtCreateUserProcess:return  [Caller SearchIndexer.]: Time taken to return from create process is 137961 MicroSecond

```

## <a name="file-delete-tracker"></a>ファイル削除トラッカー

このサンプルスクリプトでは、syscall プロバイダーを使用して、入力時に NtOpenFile をインストルメントし、渡されたフラグ (引数 #5) を確認して、システム全体の削除を追跡します。

次のスクリプトを filedeletetracker. d にコピーします。

```dtrace
ERROR{exit(0);}

struct ustr{uint16_t buffer[256];};

syscall::NtOpenFile:entry
{
   this->deleted = arg5 & 0x00001000; /* & with FILE_DELETE_ON_CLOSE */

  if (this->deleted) {
        this->attr = (nt`_OBJECT_ATTRIBUTES*)
            copyin(arg2, sizeof(nt`_OBJECT_ATTRIBUTES));

        if (this->attr->ObjectName) {
            this->objectName = (nt`_UNICODE_STRING*)
                copyin((uintptr_t)this->attr->ObjectName,
                       sizeof(nt`_UNICODE_STRING));
          
            this->fname = (uint16_t*)
                copyin((uintptr_t)this->objectName->Buffer,
                       this->objectName->Length);

            printf("Process %s PID %d deleted file %*ws \n", execname,pid, 
            this->objectName->Length / 2, 
             ((struct ustr*)this->fname)->buffer);
        }
    }
}
```

テストスクリプトを実行するには、-s オプションを使用します。

削除するファイルを作成または検索します。 ファイルをごみ箱に移動し、ごみ箱を空にします。 ファイルが削除され、イベントが発生して、ファイルの削除に関する情報が表示されます。

```dtrace
C:\Windows\system32>dtrace -s filedeletetracker.d
dtrace: script 'filedeletetracker.d' matched 8 probes
CPU     ID                    FUNCTION:NAME
  0    512                 NtOpenFile:entry Process explorer.exe PID 4684 deleted file \??\C:\$Recycle.Bin\S-1-12-1-3310478672-1302480547-4207937687-2985363607\$ROSR3FA.txt
```

このプログラムは、ファイルの削除を引き続き監視するように設計されています。 CTRL + C キーを押して終了します。

さらに大きなコードサンプルについては、次の「 [DTrace Windows コードサンプル](dtrace-code-samples.md)」を参照してください。

## <a name="see-also"></a>参照

[Windows 上の DTrace](dtrace.md)

[DTrace ETW](dtrace-etw.md)

[DTrace Windows コードサンプル](dtrace-code-samples.md)

[DTrace ライブダンプ](dtrace-live-dump.md)
