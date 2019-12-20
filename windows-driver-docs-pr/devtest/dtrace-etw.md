---
title: DTrace ETW
description: DTrace では、D プログラミング言語を使用した Windows イベントトレーシング (ETW) がサポートされています。
ms.assetid: abf23d76-423d-4d1e-afde-83739015bbf1
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
ms.openlocfilehash: cf77440157fa3cad5f7e4acf2cbb42bdab02119d
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209478"
---
# <a name="dtrace-etw"></a>DTrace ETW

Windows 用の DTrace を使用して、既存の ETW イベントを処理し、新しい ETW イベントを追加します。

Windows イベントトレーシング (ETW) はカーネルレベルのトレース機能であり、カーネルまたはアプリケーションによって定義されたイベントをログファイルに記録できます。 イベントは、リアルタイムで使用することも、ログファイルから使用して、アプリケーションをデバッグしたり、アプリケーションでパフォーマンスの問題が発生している場所を確認したりすることもできます。 ETW に関する一般的な情報については、「[イベントトレースについ](https://docs.microsoft.com/windows/win32/etw/about-event-tracing)て」を参照してください。

> [!NOTE]
> DTrace は、バージョン18980および Windows Server Insider Preview ビルド18975以降の Windows の Insider ビルドでサポートされています。

Windows での DTrace の使用に関する一般的な情報については、「 [dtrace](dtrace.md)」を参照してください。

## <a name="etw-windows-dtrace-provider"></a>ETW Windows DTrace プロバイダー

DTrace を使用して、トレースログとマニフェストベースの ETW イベントをキャプチャし、レポートすることができます。 特定のキーワード/レベル/警告 ~ をプローブするために、ワイルドカードを使用しない場合、ETW プローブはより確実に動作します。 代わりに、次の規則に基づいてプローブを完全に指定します。  

Probename = etw

Modname は、すべての小文字を使用する xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx 形式のプロバイダー guid です。

Funcname = フォーム0x00_0x0000000000000000 の Level_Keyword。 すべてを一致させるには、これを0xff_0xffffffffffffffff に設定する必要があります。

Probename = 整数イベント ID または "generic_event" は、すべてのイベント Id に一致します。

Probename に基づくフィルター処理は、イベントの発生に対してのみ機能します。 トレースログイベントには、ワイルドカード (*) を使用します。

ETW ペイロードには、arg0 経由でアクセスします。 これは nt\`\_イベント\_ヘッダーの後にイベント固有の日付が続く形式で構成されます。

### <a name="determining-available-etw-providers"></a>利用可能な ETW プロバイダーの特定

Logman コマンドを使用して、アクティブな ETW プロバイダーとそのプロバイダー Guid を表示します。

```dtrace
C:\>logman query providers
...
Microsoft-Windows-Kernel-Memory {D1D93EF7-E1F2-4F45-9943-03D245FE6C00}
Microsoft-Windows-Kernel-Network {7DD42A49-5329-4832-8DFD-43D979153A88}
Microsoft-Windows-Kernel-PnP {9C205A39-1250-487D-ABD7-E831C6290539}
Microsoft-Windows-Kernel-Power {331C3B3A-2005-44C2-AC5E-77220C37D6B4}
Microsoft-Windows-Kernel-Prefetch {5322D61A-9EFA-4BC3-A3F9-14BE95C144F8}
Microsoft-Windows-Kernel-Process {22FB2CD6-0E7B-422B-A0C7-2FAD1FD0E716}
...
```

## <a name="displaying-existing-etw-provider-information"></a>既存の ETW プロバイダー情報を表示しています

DTrace には、ETW イベントを出力する機能があります。 これは、レポート、収集、および分析を行う既存の ETW パイプラインがある場合に便利です。

この例の DTrace コマンドを使用して、Microsoft Windows のカーネルメモリプロバイダーのイベントを報告します。

```dtrace
C:\>dtrace -n "etw:d1d93ef7-e1f2-4f45-9943-03d245fe6c00:0xff_0xffffffffffffffff:12"
dtrace: description 'etw:d1d93ef7-e1f2-4f45-9943-03d245fe6c00:0xff_0xffffffffffffffff:12' matched 1 probe
CPU     ID                    FUNCTION:NAME
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
  0   3271       0xff_0xffffffffffffffff:12
```

## <a name="adding-new-etw-events"></a>新しい ETW イベントを追加しています

Etw トレースイベントは、etw\_トレースマクロを呼び出すことによって作成できます。 イベントは、指定されたトレースプロバイダーのアクティブなリスナーが存在する場合にのみログに記録されます。それ以外の場合、イベントはスキップされます。

Etw\_trace マクロは、int8、uint8、int16、uint16、int32、uint32、int64、uint64、hexint32、hexint64、string などの基本的なデータ型をサポートしています。 詳細については、以下の「*サポートされている ETW データ型*」の表を参照してください。

**ETW\_トレースマクロの例:**

このスクリプトは、syscall ルーチンから 0xc0000001-STATUS_UNSUCCESSFUL が返されたときに、カスタム ETW イベントを生成します。

`this->status` 値を変更して別の[NTSTATUS 値](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)を使用して、さまざまな syscall の戻り値をログに記録することができます。

```dtrace
syscall:::return 
{ 
    this->status = (uint32_t) arg0;

    if (this->status == 0xc0000001UL) 
    { 
        etw_trace
        (
            "Tools.DTrace.Platform", /* Provider Name */
            "AAD330CC-4BB9-588A-B252-08276853AF02", /* Provider GUID */
            "My custom event from DTrace", /* Event Name */
            1, /* Event Level (0 - 5) */
            0x0000000000000020, /* Flag */
            "etw_int32", /* Field_1 Name */
            "PID",/* Field_1 Type */
            (int32_t)pid, /* Field_1 Value  */
            "etw_string", /* Field_2 Name */
            "Execname", /* Field_2 type */
            execname, /* Field_2 Value */
            "etw_string", /* Field_3 Name */
            "Probefunc", /* Field_3 type */
            probefunc /* Field_3 Value */   
            );
    }
}
```

```dtrace
C:\> dtrace -s addnewetwevent.d
dtrace: script 'addnewetwevent.d' matched 1881 probes
CPU     ID                    FUNCTION:NAME
  0     93 NtAlpcSendWaitReceivePort:return
  0     93 NtAlpcSendWaitReceivePort:return
  0     93 NtAlpcSendWaitReceivePort:return
```

## <a name="etw-numa-mem-stats-example-code"></a>ETW NUMA メモリ STATS サンプルコード

このサンプルスクリプトでは、Microsoft-Windows-カーネルの ETW プロバイダーを使用して、NUMA ノードのメモリをダンプします。 ページサイズは、4を乗算することによって、サイズを KB 単位に変換できます。 NUMA に関する一般的な情報については、「 [Numa サポート](https://docs.microsoft.com/windows/win32/procthread/numa-support)」を参照してください。

このコードは、「」にもあり <https://github.com/microsoft/DTrace-on-Windows/blob/master/samples/windows/etw/numamemstats.d>

```dtrace
typedef struct KernelMemInfoEvent
{
        struct nt`_EVENT_HEADER _EH;
    uint32_t PartitionId;
    uint32_t Count;
    uint32_t NodeNumber;
}kmi;

typedef struct MemoryNodeInfo
{
    uint64_t TotalPageCount;
    uint64_t SmallFreePageCount;
    uint64_t SmallZeroPageCount;
    uint64_t MediumFreePageCount;
    uint64_t MediumZeroPageCount;
    uint64_t LargeFreePageCount;
    uint64_t LargeZeroPageCount;
    uint64_t HugeFreePageCount;
    uint64_t HugeZeroPageCount;
}m_nodeinfo;

int printcounter;

BEGIN
{
    printcounter = 0;
}

/* MemNodeInfo */
etw:d1d93ef7-e1f2-4f45-9943-03d245fe6c00:0xff_0xffffffffffffffff:12
{
    if (printcounter%10 == 0)
    {
        printf ("\n \n");
        printf("Partition ID: %d \n",((kmi *)arg0)->PartitionId);
        printf("Count: %d \n", ((kmi *)arg0)->Count);
        
        printf("Node number: %d\n", ((kmi *)arg0)->NodeNumber);
        counters = (m_nodeinfo*)(arg0 + sizeof(struct nt`_EVENT_HEADER) + 12);
        print(*counters);

        /* Dump rest of the NUMA node info */

        if (((kmi *)arg0)->Count > 1)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(1)) + (sizeof(uint32_t)*(1)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(1)) + (sizeof(uint32_t)*(1)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 2)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(2)) + (sizeof(uint32_t)*(2)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(2)) + (sizeof(uint32_t)*(2)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 3)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(3)) + (sizeof(uint32_t)*(3)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(3)) + (sizeof(uint32_t)*(3)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 4)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(4)) + (sizeof(uint32_t)*(4)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(4)) + (sizeof(uint32_t)*(4)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 5)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(5)) + (sizeof(uint32_t)*(5)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(5)) + (sizeof(uint32_t)*(5)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 6)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(6)) + (sizeof(uint32_t)*(6)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(6)) + (sizeof(uint32_t)*(6)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 7)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(7)) + (sizeof(uint32_t)*(7)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(7)) + (sizeof(uint32_t)*(7)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 8)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(8)) + (sizeof(uint32_t)*(8)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(8)) + (sizeof(uint32_t)*(8)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 9)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(9)) + (sizeof(uint32_t)*(9)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(9)) + (sizeof(uint32_t)*(9)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 10)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(10)) + (sizeof(uint32_t)*(10)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(10)) + (sizeof(uint32_t)*(10)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 11)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(11)) + (sizeof(uint32_t)*(11)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(11)) + (sizeof(uint32_t)*(11)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 12)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(12)) + (sizeof(uint32_t)*(12)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(12)) + (sizeof(uint32_t)*(12)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 13)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(13)) + (sizeof(uint32_t)*(13)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(13)) + (sizeof(uint32_t)*(13)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 14)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(14)) + (sizeof(uint32_t)*(14)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(14)) + (sizeof(uint32_t)*(14)) + sizeof(uint32_t));
            print(*counters);
        }
        if (((kmi *)arg0)->Count > 15)
        {
            nodenumber = (uint32_t *) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(15)) + (sizeof(uint32_t)*(15)) );
            printf ("Node Number: %d \n", *nodenumber);
            counters = (m_nodeinfo*) (arg0 + sizeof(struct nt`_EVENT_HEADER) + 8 + (sizeof(m_nodeinfo)*(15)) + (sizeof(uint32_t)*(15)) + sizeof(uint32_t));
            print(*counters);
        }

    }
    exit(1);
    printcounter++;
}
```

ファイルを etwnumamemstats. d として保存します。

管理者としてコマンドプロンプトを開き、-s オプションを使用してスクリプトを実行します。 

クライアントの Windows PC で実行している場合は、1つの NUMA ノードが表示されます。

```dtrace
C:\> dtrace -s etwnumamemstats.d
trace: script 'etwnumamemstats.d' matched 36 probes
CPU     ID                    FUNCTION:NAME
  0  42735       0xff_0xffffffffffffffff:12

Partition ID: 0
Count: 1
Node number: 1
m_nodeinfo {
    uint64_t TotalPageCount = 0xab98d
    uint64_t SmallFreePageCount = 0
    uint64_t SmallZeroPageCount = 0x1bec
    uint64_t MediumFreePageCount = 0
    uint64_t MediumZeroPageCount = 0x5a
    uint64_t LargeFreePageCount = 0
    uint64_t LargeZeroPageCount = 0
    uint64_t HugeFreePageCount = 0
    uint64_t HugeZeroPageCount = 0
}
  0  42735       0xff_0xffffffffffffffff:12
```

## <a name="supported-etw-data-types"></a>サポートされている ETW データ型

| **ETW の種類**           | **D 言語のデータ型** | **メモ**                                                                                 |
| ---------------------- | ------------------------ | ----------------------------------------------------------------------------------------- |
| etw\_構造体            | 整数型                  | この型のペイロード値は、新しい構造体が持つメンバーの数を表します。  |
| etw\_文字列            | string                   | 該当なし                                                                                       |
| etw\_mbcsstring        | string                   | 該当なし                                                                                       |
| etw\_int8              | 整数型                  | 型のサイズが一致する必要があります。また、D スクリプトで \`int8\_t\` にキャストすることをお勧めします。             |
| etw\_uint8             | 整数型                  | 型のサイズは一致する必要があり、D スクリプトで \`uint8\_t\` にキャストすることをお勧めします。            |
| etw\_int16             | 整数型                  | 型のサイズは一致する必要があり、\`int16 にキャスト\_t\` にキャストします。            |
| etw\_uint16            | 整数型                  | 型のサイズが一致する必要があります。また、D スクリプトで \`uint16\_t\` にキャストすることをお勧めします。           |
| etw\_int32             | 整数型                  | 該当なし                                                                                       |
| etw\_uint32            | 整数型                  | 該当なし                                                                                       |
| etw\_int64             | 整数型                  | D の既定値は \`int32\_t であるため、型は明示的に int64\`\_\`にする必要があり\`                  |
| etw\_uint64            | 整数型                  | D の既定値は \`int32\_t であるため、型は明示的に int64\`\_\`にする必要があり\`                  |
| etw\_float             | Scalar                   | 浮動小数点定数は D スクリプトでは許可されていませんが、読み込まれたシンボルでは使用できます |
| etw\_double            | Scalar                   | 浮動小数点定数は D スクリプトでは許可されていませんが、読み込まれたシンボルでは使用できます |
| etw\_bool32            | 整数型                  | 該当なし                                                                                       |
| etw\_hexint32          | 整数型                  | 該当なし                                                                                       |
| etw\_hexint64          | 整数型                  | D の既定値は \`int32\_t であるため、型は明示的に int64\`\_\`にする必要があり\`                  |
| etw\_countedmbcsstring | 整数型                  | 該当なし                                                                                       |
| etw\_intptr            | 整数型                  | データ型のサイズは、アーキテクチャに応じて変化します (\`int32\_t\` vs \`int64\_t\`)   |
| etw\_uintptr           | 整数型                  | データ型のサイズは、アーキテクチャに応じて変化します (\`int32\_t\` vs \`int64\_t\`)   |
| etw\_ポインター           | 整数型                  | データ型のサイズは、アーキテクチャに応じて変化します (\`int32\_t\` vs \`int64\_t\`)   |
| etw\_char16            | 整数型                  | 型のサイズは一致する必要があり、\`int16 にキャスト\_t\` にキャストします。            |
| etw\_char8             | 整数型                  | 型のサイズが一致する必要があります。また、D スクリプトで \`int8\_t\` にキャストすることをお勧めします。             |
| etw\_bool8             | 整数型                  | 型のサイズが一致する必要があります。また、D スクリプトで \`int8\_t\` にキャストすることをお勧めします。             |
| etw\_hexint8           | 整数型                  | 型のサイズが一致する必要があります。また、D スクリプトで \`int8\_t\` にキャストすることをお勧めします。             |
| etw\_hexint16          | 整数型                  | 型のサイズは一致する必要があり、\`int16 にキャスト\_t\` にキャストします。            |
| etw\_pid               | 整数型                  | 該当なし                                                                                       |
| etw\_tid               | 整数型                  | 該当なし                                                                                       |
| etw\_mbcsxml           | 整数型                  | 該当なし                                                                                       |
| etw\_mbcsjson          | 整数型                  | 該当なし                                                                                       |
| etw\_countedmbcsxml    | 整数型                  | 該当なし                                                                                       |
| etw\_countedmbcsjson   | 整数型                  | 該当なし                                                                                       |
| etw\_win32error        | 整数型                  | 該当なし                                                                                       |
| etw\_ntstatus          | 整数型                  | 該当なし                                                                                       |
| etw\_hresult           | 整数型                  | 該当なし                                                                                       |

## <a name="see-also"></a>参照

[Windows 上の DTrace](dtrace.md)

[DTrace の Windows プログラミング](dtrace-programming.md)

[DTrace Windows コードサンプル](dtrace-code-samples.md)

[DTrace ライブダンプ](dtrace-live-dump.md)
