---
title: DTrace コードサンプル
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
ms.openlocfilehash: 6457c7d9690c83ec52b62719e8d3169e96ca4077
ms.sourcegitcommit: 5081de283b09b4fe847912fc1dc0e7f057e0a0cd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73592429"
---
# <a name="dtrace-code-samples"></a>DTrace コードサンプル

DTrace は、D プログラミング言語をサポートしています。 このトピックでは、D コードサンプルについて説明します。

Windows 上の DTrace に関する一般的な情報については、「 [dtrace](dtrace.md)」を参照してください。

DTrace の詳細については、ケンブリッジの大学の[OpenDTrace 仕様バージョン 1.0](https://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-924.pdf)を参照してください。

> [!NOTE]
> DTrace は、バージョン18980および Windows Server Insider Preview ビルド18975以降の Windows の Insider ビルドでサポートされています。

## <a name="additional-sample-scripts"></a>その他のサンプルスクリプト

Windows のシナリオに適用される追加の D スクリプトは、DTrace ソースコードの samples ディレクトリにあります。

[https://github.com/microsoft/DTrace-on-Windows/tree/master/samples/windows](https://github.com/microsoft/DTrace-on-Windows/tree/master/samples/windows)

一連の便利な opentrace toolkit スクリプトは、 [https://github.com/opendtrace/toolkit](https://github.com/opendtrace/toolkit)で入手できます。


## <a name="disk-usage-by-name"></a>名前によるディスク使用量

このスクリプトは、特定の実行可能ファイル名のディスクカウンターを提供します。 実行可能ファイル名は大文字と小文字が区別され、スクリプトの起動時にコマンドラインに表示されます。

```dtrace

#pragma D option quiet
#pragma D option destructive


intptr_t curptr;
struct nt`_EPROCESS *eprocess_ptr;
int found;
int firstpass;
BEGIN
{
    curptr = (intptr_t) ((struct nt`_LIST_ENTRY *) (void*)&nt`PsActiveProcessHead)->Flink;  
    found = 0;
    firstpass = 1;
    bytesread = 0;
    byteswrite = 0;
    readcount = 0;
    writecount = 0;
    flushcount = 0;
}

tick-1ms

/found == 0/

{
/* use this for pointer parsing */
    if (found == 0)
    {
        eprocess_ptr = (struct nt`_EPROCESS *)(curptr - offsetof(nt`_EPROCESS, ActiveProcessLinks));
        processid = (string) eprocess_ptr->ImageFileName;

        if ($1 == processid)
        {
            found = 1;
        }

        else 
        {
            curptr = (intptr_t) ((struct nt`_LIST_ENTRY *) (void*)curptr)->Flink;
        }
    }       
}

tick-2s

{
    system ("cls");
    if (found == 1)
    {
        if (firstpass)
        {
            firstpass = 0;
            bytesread = (unsigned long long) eprocess_ptr->DiskCounters->BytesRead;
            byteswrite = (unsigned long long) eprocess_ptr->DiskCounters->BytesWritten;
            readcount = eprocess_ptr->DiskCounters->ReadOperationCount;
            writecount = eprocess_ptr->DiskCounters->WriteOperationCount;
            flushcount =  eprocess_ptr->DiskCounters->FlushOperationCount;
        }

        else
        {
            bytesread = (unsigned long long)  (eprocess_ptr->DiskCounters->BytesRead - bytesread);
            byteswrite = (unsigned long long)  (eprocess_ptr->DiskCounters->BytesWritten - byteswrite);
            readcount = eprocess_ptr->DiskCounters->ReadOperationCount - readcount;
            writecount = eprocess_ptr->DiskCounters->WriteOperationCount - writecount;      
            flushcount = eprocess_ptr->DiskCounters->FlushOperationCount - flushcount;

            printf("*** Reports disk read/write every second *** \n");
            printf("Process name: %s\n", eprocess_ptr->ImageFileName);
            printf("Process Id: %d\n", (int) eprocess_ptr->UniqueProcessId);
            printf("Bytes Read %llu \n",  (unsigned long long) bytesread);
            printf("Bytes Written %llu \n", (unsigned long long) byteswrite);
            printf("Read Operation Count %d \n", readcount);
            printf("Write Operation Count %d \n",writecount);
            printf("Flush Operation Count %d \n", flushcount);

            bytesread = (unsigned long long) eprocess_ptr->DiskCounters->BytesRead;
            byteswrite = (unsigned long long) eprocess_ptr->DiskCounters->BytesWritten;
            readcount = eprocess_ptr->DiskCounters->ReadOperationCount;
            writecount = eprocess_ptr->DiskCounters->WriteOperationCount;
            flushcount =  eprocess_ptr->DiskCounters->FlushOperationCount;      
        }       
    }

    else
    {
        printf("No matching process found for %s \n", $1);
        exit(0);
    }
}
```

ファイルを diskuagebyname として保存し、-s オプションを使用してテストスクリプトを実行します。 Notepad.exe などの目的の exe の名前を大文字と小文字を区別して指定します。

```dtrace

C:\>dtrace -s diskusagebyname.d Notepad.exe

*** Reports disk read/write every second *** 
Process name: Notepad.exe
Process Id: 6012
Bytes Read 0 
Bytes Written 0 
Read Operation Count 0 
Write Operation Count 0 
Flush Operation Count 0 
*** Reports disk read/write every second *** 
Process name: cmd.exe
Process Id: 4428
Bytes Read 18446744073709480960 
Bytes Written 18446744073709522944 
Read Operation Count -5 
Write Operation Count -7 
Flush Operation Count 0 

```

ディスクアクティビティの実行中のログを保持するには、次に示すように、コマンドをテキストファイルにリダイレクトします。

```dtrace
C:\>dtrace -s diskusagebyname.d Notepad.exe>>diskstats.txt
```

## <a name="dumping-memory-usage"></a>ダンプ (メモリ使用量を)

一部の診断ケースでは、状況を理解するためにカーネル構造をダンプする必要があります。 このコードは、システムのメモリ使用量をダンプする例を示しています。 次の D スクリプトは、3秒ごとにタイマープローブを起動し、システムのメモリ使用量を更新します。

```dtrace
#pragma D option quiet
#pragma D option destructive

tick-3s
{
    system ("cls");

    this->pp = ((struct nt`_MI_PARTITION *) &nt`MiSystemPartition);

    printf("***** Printing System wide page information ******* \n");
    printf( "Total Pages Entire Node: %u MB \n", this->pp->Core.NodeInformation->TotalPagesEntireNode*4096/(1024*1024));
    printf("Total Available Pages: %u Mb \n", this->pp->Vp.AvailablePages*4096/(1024*1024));
    printf("Total ResAvail Pages: %u  Mb \n",  this->pp->Vp.ResidentAvailablePages*4096/(1024*1024));
    printf("Total Shared Commit: %u  Mb \n",  this->pp->Vp.SharedCommit*4096/(1024*1024));
    printf("Total Pages for PagingFile: %u  Mb \n",  this->pp->Vp.TotalPagesForPagingFile*4096/(1024*1024));
    printf("Modified Pages : %u  Mb \n",  this->pp->Vp.ModifiedPageListHead.Total*4096/(1024*1024));
    printf("Modified No Write Page Count : %u  Mb \n",  this->pp->Vp.ModifiedNoWritePageListHead.Total*4096/(1024*1024));
    printf("Bad Page Count : %d  Mb \n",  this->pp->PageLists.BadPageListHead.Total*4096/(1024*1024));
    printf("Zero Page Count : %d  Mb \n",  this->pp->PageLists.ZeroedPageListHead.Total*4096/(1024*1024));
    printf("Free Page Count : %d  Mb \n",  this->pp->PageLists.FreePageListHead.Total*4096/(1024*1024));


/********** Printing Commit info ******************/ 
    
    this->commit = ((struct nt`_MI_PARTITION_COMMIT ) ((struct nt`_MI_PARTITION *) &nt`MiSystemPartition)->Commit);

    printf("***** Printing Commit Info ******* \n");
    printf("Total Committed Pages: %u  Mb \n", this->pp->Vp.TotalCommittedPages*4096/(1024*1024));
    printf("Total Commit limit: %u  Mb  \n", this->pp->Vp.TotalCommitLimit*4096/(1024*1024));
    printf("Peak Commitment: %u Mb \n", this->commit.PeakCommitment*4096/(1024*1024));
    printf("Low Commit Threshold: %u Mb \n", this->commit.LowCommitThreshold*4096/(1024*1024));
    printf("High Commit Threshold: %u Mb \n", this->commit.HighCommitThreshold*4096/(1024*1024));
    printf("System Commit Reserve: %u Mb \n", this->commit.SystemCommitReserve*4096/(1024*1024));
    

}
```

ファイルを dumpmemoryusage. d として保存します。

このサンプルではシンボルを使用しているため、「インストール」で説明されているように、シンボルパスを設定します。

```cmd
set _NT_SYMBOL_PATH=srv*C:\symbols*https://msdl.microsoft.com/download/symbols 
```
テストスクリプトを実行するには、-s オプションを使用します。

```dtrace
C:\>dtrace -s dumpmemoryusage.d
***** Printing System wide page information ******* 
Total Pages Entire Node: 2823 MB 
Total Available Pages: 622 Mb 
Total ResAvail Pages: 2369  Mb 
Total Shared Commit: 166  Mb 
Total Pages for PagingFile: 30  Mb 
Modified Pages : 30  Mb 
Modified No Write Page Count : 0  Mb 
Bad Page Count : 0  Mb 
Zero Page Count : 7  Mb 
Free Page Count : 0  Mb 
***** Printing Commit Info ******* 
Total Committed Pages: 2401  Mb 
Total Commit limit: 4551  Mb  
Peak Commitment: 2989 Mb 
Low Commit Threshold: 3413 Mb 
High Commit Threshold: 4295 Mb 
System Commit Reserve: 5 Mb 
```

このプログラムは、メモリ使用量を引き続き監視するように設計されています。 CTRL + C キーを押して終了します。

## <a name="identifying-heap-free-time-breakdown-for-an-activity"></a>アクティビティのヒープの空き時間内訳の特定

このサンプルでは、サブ関数に[Rtlfreeheap](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlfreeheap)関数を分解し、これらの関数の実行にかかった最大時間を表示します。

```dtrace
/* Mark script destructive as we call "cls" in the tick-1sec provider*/
#pragma D option destructive

/* Program to calculate time taken in RtlFreeHeap function. Hit Ctrl-C to break. */ 

dtrace:::BEGIN 
{
    counter1 = 0;

}

tick-1sec
{
    system ("cls");
    printf("count of function hit = %d << Press Ctrl-C to exit >> \n", counter1);

}

/* Instrument entry of RtlFreeHeap*/

pid$1:ntdll:RtlFreeHeap:entry
{ 
    /* self is thread local */
    self->ts = timestamp;
    self->depth = 0;
    counter1++;
} 

pid$1:ntdll:RtlFreeHeap:return
/self->ts/
{
    this->ts = timestamp - self->ts;
    @disttime = quantize(this->ts); 
    @funcName[probemod,probefunc] = max(this->ts);  
    self->ts = 0;
}


pid$1:::entry
/ self->ts /
{
    self->functime[self->depth] = timestamp;
    self->depth++;
}

pid$1:::return
/ self->ts /
{
    if (self->depth > 0)
    {
        self->depth--;
        /* this is a local scope */
        this->ts = timestamp - self->functime[self->depth];
        @funcName[probemod,probefunc] = max(this->ts);
    }
}

END

{
    system ("cls");
    /* Print overall time distribution for RtlFreeHeap */
    printa (@disttime);
    /* Print top 15 functions along with average time spent executing them */
    trunc (@funcName, 15);
    
    printa( @funcName);
    
}

```

ファイルを heapfree. d として保存します。

このスクリプトは、プロセス ID または PID を受け取ります。 スクリプトをテストするには、コマンドプロンプトで tasklist を実行し、目的の PID を見つけます。

```dtrace
C:\>tasklist

Image Name                     PID Session Name        Session#    Mem Usage
========================= ======== ================ =========== ============
System Idle Process              0 Services                   0          8 K
System                           4 Services                   0        108 K
Registry                        72 Services                   0     35,576 K

...

Notepad.exe                   7944 31C5CE94259D4006           2     20,736 K

```

パラメーターとして PID を指定し、以下に示すように-s オプションを使用してテストスクリプトを実行します。

```dtrace
C:\>dtrace -s heapfree.d 7944

count of function hit = 28 <<Press Ctrl-C to exit>>
```

メモ帳での入力やフォントの変更など、PID に関連付けられているプログラムで、どのような作業が必要かを実行します。

CTRL キーを押しながら C キーを押すと、ヒープの使用状況がスタック情報と共に表示されます。

```dtrace
           value  ------------- Distribution ------------- count
            4096 |                                         0
            8192 |@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@        23
           16384 |@@@@@@                                   4
           32768 |                                         0
           65536 |                                         0
          131072 |@                                        1
          262144 |                                         0


  ntdll                                               RtlTryEnterCriticalSection                                     9444
  ntdll                                               RtlGetCurrentServiceSessionId                                 12302
  ntdll                                               RtlFreeHeap                                                  151354
  ```

## <a name="memory-pool-tracking"></a>メモリプールの追跡

注: このスクリプトは、aggsortkeypos 変数 set を使用して実行してください。 この変数は、最初のインデックス (サイズ) に基づいて出力を並べ替えるように、D トレースに通知します。

使い方:

`dtrace -s <script.d>  <Time> <Tag> -x  aggsortkey -x aggsortkeypos=1` 

KSec リークの追跡の例: dtrace-s PoolTrackingSummary. d "120s" 0x6365734b-x aggsortkey-x aggsortkeypos = 1 

`<Tag>` 値は、メモリプールタグのエンコードされた ASCII 値です。 たとえば、nt ファイルシステムのタグ値 (NtFf) をエンコードするには、最初に2つの文字セットを逆にし、fFtN にします。 ASCII 文字を16進形式に変換すると、46 66 74 4e、またはプログラムのパラメーターとして0x4666744e になります。

もう1つの例では、Ksec を変換します。

最初に文字の順序を逆にします: cesK

次に、プログラムのパラメーターとして、これらの文字を16進、63 65 73 4b、または0x6365734b に変換します。

プールタグに一致させるには、大文字と小文字の区別が重要であることに注意してください。

出力: スクリプトは120秒間実行され、KSec の割り当て/解放の概要が出力されます。 これは、必要な時間に設定できます。

```dtrace
#pragma D option destructive
#pragma D option quiet
#pragma D option dynvarsize=240m 
#pragma D option bufsize=120m
#pragma D option aggsize=120m 


fbt:nt:ExAllocatePoolWithTag:entry
{   
    /* This is E100 in reserve. Convert ASCII to Hex => Hex('001E').*/
    if (arg2 == $2) 
    { 
        self->size = (unsigned int) arg1;
        @allocstack[stack(), self->size] = count();
    }
}

fbt:nt:ExAllocatePoolWithTag:return
/self->size/
{
    @mem[(uintptr_t) arg1] = sum(1);
    addr[(uintptr_t) arg1] = 1;
    /* printf("%Y: Execname %s allocated size %d bytes return ptr %x", walltimestamp, execname, (uint64_t) self->size, (uintptr_t) arg1 );*/

    size[(uintptr_t) arg1] = self->size;
    @sizealloc[self->size] = count();
    @delta[self->size] = sum(1);
    
    self->size = 0;
}

fbt:nt:ExFreePoolWithTag:entry
/addr[(uintptr_t) arg0]/
{
    @mem[(uintptr_t) arg0] = sum (-1);
    addr[(uintptr_t) arg0] -= 1;

    @sizefree[size[(uintptr_t) arg0]] = count();
    @delta[size[(uintptr_t) arg0]] = sum(-1);
}

tick-$1
{   
    exit(0);
}

END 
{

   printf("%10s %10s %10s %10s\n", "SIZE", "ALLOC", "FREE", "DELTA");
   printa("%10d %@10d %@10d %@10d\n", @sizealloc, @sizefree, @delta);

   printf("Printing stacks \n");
   printa (@allocstack);
    
   printf("== REPORT ==\n\n");
   printa("0x%x => %@u\n",@mem);
}

```

ファイルを pooltrackingsummary. d として保存し、-s オプションを使用してテストスクリプトを実行します。これには、上記で説明したタグ値とその他のパラメーターを指定します。

120s オプションでは、プログラムは2分間実行されます。 その間、Windows を使用して、監視対象のメモリプールを実行します。 たとえば、web ブラウザーやその他のプログラムを読み込んでアンロードします。

```dtrace
C:\>dtrace -s pooltrackingsummary.d "120s" 0x4666744e -x aggsortkey -x aggsortkeypos=1
      SIZE      ALLOC       FREE      DELTA
      1552         16          0         16
Printing stacks

              Ntfs.sys`NtfsCreateFcb+0x388
              Ntfs.sys`NtfsCreateNewFile+0xaa8
              Ntfs.sys`NtfsCommonCreate+0x2303
              Ntfs.sys`NtfsFsdCreate+0x284
              nt`IofCallDriver+0x55
              FLTMGR.SYS`FltpLegacyProcessingAfterPreCallbacksCompleted+0x1b9
              FLTMGR.SYS`FltpCreate+0x324
              nt`IofCallDriver+0x55
              nt`IoCallDriverWithTracing+0x34
              nt`IopParseDevice+0x6ac
              nt`ObpLookupObjectName+0x3fe
              nt`ObOpenObjectByNameEx+0x1fa
              nt`IopCreateFile+0x40f
              nt`NtCreateFile+0x79
              nt`KiSystemServiceCopyEnd+0x38
     1552                3

              Ntfs.sys`NtfsCreateFcb+0x388
              Ntfs.sys`NtfsOpenFile+0x2d7
              Ntfs.sys`NtfsCommonCreate+0x25a8
              Ntfs.sys`NtfsFsdCreate+0x284
              nt`IofCallDriver+0x55
              FLTMGR.SYS`FltpLegacyProcessingAfterPreCallbacksCompleted+0x1b9
              FLTMGR.SYS`FltpCreate+0x324
              nt`IofCallDriver+0x55
              nt`IoCallDriverWithTracing+0x34
              nt`IopParseDevice+0x6ac
              nt`ObpLookupObjectName+0x3fe
              nt`ObOpenObjectByNameEx+0x1fa
              nt`IopCreateFile+0x40f
              nt`NtCreateFile+0x79
              nt`KiSystemServiceCopyEnd+0x38
     1552                4

              Ntfs.sys`NtfsCreateFcb+0x388
              Ntfs.sys`NtfsOpenFile+0x2d7
              Ntfs.sys`NtfsCommonCreate+0x25a8
              Ntfs.sys`NtfsFsdCreate+0x284
              nt`IofCallDriver+0x55
              FLTMGR.SYS`FltpLegacyProcessingAfterPreCallbacksCompleted+0x1b9
              FLTMGR.SYS`FltpCreate+0x324
              nt`IofCallDriver+0x55
              nt`IoCallDriverWithTracing+0x34
              nt`IopParseDevice+0x6ac
              nt`ObpLookupObjectName+0x3fe
              nt`ObOpenObjectByNameEx+0x1fa
              nt`IopCreateFile+0x40f
              nt`NtOpenFile+0x58
              nt`KiSystemServiceCopyEnd+0x38
     1552                3

...

== REPORT ==

0xffffd304c98dd380 => 1
0xffffd304cc4655a0 => 1
0xffffd304cccf15a0 => 1
0xffffd304ccdeb990 => 1
0xffffd304ce048760 => 1
0xffffd304cf1ee990 => 1
0xffffd304d0473010 => 1
0xffffd304d12075a0 => 1
0xffffd304d14135a0 => 1
0xffffd304d1674010 => 1
0xffffd304d33b3660 => 1
0xffffd304d3b29010 => 1
0xffffd304d42c6010 => 1
0xffffd304d48b2010 => 1
0xffffd304de1fa5f0 => 1
0xffffd304e1ad56a0 => 1
```

## <a name="comparing-guids"></a>Guid の比較

DTrace では GUID がネイティブにサポートされていませんが、このサンプルコードで示すように構造体を作成して操作することができます。 ここでは、Guid を比較する方法の例を示します。

```dtrace
nt`_GUID guidcmp;


/* Sleep After GUID: 29f6c1db-86da-48c5-9fdb-f2b67b1f44da */
dtrace:::BEGIN
{
    printf("Begin\n");
    guidcmp.Data1 = 0x29f6c1db;
    guidcmp.Data2 = 0x86da;
    guidcmp.Data3 = 0x48c5;
    guidcmp.Data4[0] = 0x9f;
    guidcmp.Data4[1]  = 0xdb;
    guidcmp.Data4[2]  = 0xf2;
    guidcmp.Data4[3]  = 0xb6;
    guidcmp.Data4[4]  = 0x7b;
    guidcmp.Data4[5]  = 0x1f;
    guidcmp.Data4[6]  = 0x44;
    guidcmp.Data4[7]  = 0xda;
}

pid$target:PowrProf:PowerReadACValueIndexEx:entry 
{ 
    cidstr = (nt`_GUID *) (copyin(arg2, sizeof(nt`_GUID))); 

    printf("\nPrinting GUID to compare\n");
    print(guidcmp);

    printf("\nPrinting GUID received \n");
    print(*cidstr);

    if (    (cidstr->Data1 == guidcmp.Data1) &&
        (cidstr->Data2 == guidcmp.Data2) &&
        (cidstr->Data3 == guidcmp.Data3) &&
        (cidstr->Data4[0] == guidcmp.Data4[0]) &&
        (cidstr->Data4[1] == guidcmp.Data4[1]) &&
        (cidstr->Data4[2] == guidcmp.Data4[2]) &&
        (cidstr->Data4[3] == guidcmp.Data4[3]) &&
        (cidstr->Data4[4] == guidcmp.Data4[4]) &&
        (cidstr->Data4[5] == guidcmp.Data4[5]) &&
        (cidstr->Data4[6] == guidcmp.Data4[6]) &&
        (cidstr->Data4[7] == guidcmp.Data4[7])  )
    {
        printf("GUID matched \n");
    }
    else
    {
        printf("No match");
    }
}

dtrace:::END
{
    printf("End\n");
}
```

ファイルを comparequid として保存し、-s オプションを使用してテストスクリプトを実行し、次に示すパラメーターを指定します。

```dtrace
C:\Windows\system32>dtrace -s compareguid.d -c "powercfg /qh scheme_current sub_sleep standbyidle"
dtrace: script 'compareguid.d' matched 9 probes
CPU     ID                    FUNCTION:NAME
  0      1                           :BEGIN Begin
 
Power Scheme GUID: 381b4222-f694-41f0-9685-ff5bb260df2e  (Balanced)
  GUID Alias: SCHEME_BALANCED
  Subgroup GUID: 238c9fa8-0aad-41ed-83f4-97be242c8f20  (Sleep)
    GUID Alias: SUB_SLEEP
    Power Setting GUID: 29f6c1db-86da-48c5-9fdb-f2b67b1f44da  (Sleep after)
      GUID Alias: STANDBYIDLE
      Minimum Possible Setting: 0x00000000
      Maximum Possible Setting: 0xffffffff
      Possible Settings increment: 0x00000001
      Possible Settings units: Seconds
    Current AC Power Setting Index: 0x00000708
   Current DC Power Setting Index: 0x00000384
 
dtrace: pid 7560 has exited
  0  42695    PowerReadACValueIndexEx:entry
Printing GUID to compare
struct _GUID {
    UInt32 Data1 = 0x29f6c1db
    UInt16 Data2 = 0x86da
    UInt16 Data3 = 0x48c5
    UInt8 [8] Data4 = [ 0x9f, 0xdb, 0xf2, 0xb6, 0x7b, 0x1f, 0x44, 0xda ]
}
Printing GUID received
struct _GUID {
    UInt32 Data1 = 0x29f6c1db
    UInt16 Data2 = 0x86da
    UInt16 Data3 = 0x48c5
    UInt8 [8] Data4 = [ 0x9f, 0xdb, 0xf2, 0xb6, 0x7b, 0x1f, 0x44, 0xda ]
}
  0  42695    PowerReadACValueIndexEx:entry GUID matched
```

## <a name="see-also"></a>参照

[Windows 上の DTrace](dtrace.md)

[DTrace の Windows プログラミング](dtrace-programming.md)

[DTrace ETW](dtrace-etw.md)

[DTrace ライブダンプ](dtrace-live-dump.md)
