---
title: TTD メモリ オブジェクト
description: このセクションでは、タイム トラベルのデバッグに関連付けられているメモリ モデル オブジェクトについて説明します。
ms.date: 01/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: aaa9dc8d392fa4f14ef5df663bd1a657c2965502
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389111"
---
# <a name="ttd-memory-objects"></a>TTD メモリ オブジェクト
## <a name="description"></a>説明
*TTD メモリ*beginAddress、endAddress および dataAccessMask パラメーターを受け取り、メモリへのアクセス情報を格納するメモリ オブジェクトのコレクションを取得するメソッドです。

## <a name="parameters"></a>パラメーター

| プロパティ | 説明 |
| --- | --- |
| beginAddress | 0 x で始まるメモリ オブジェクトの先頭のアドレス。|
| endAddress| 0 x で始まるメモリ オブジェクトの終了アドレス。|
| dataAccessMask |二重引用符に含まれるデータのアクセス マスク。 これにより、r の読み取り、書き込み、execute e と-c は変更の w できます。 |


## <a name="children"></a>Children

| オブジェクト      | 説明 |
| ----------- | ----------- |
| EventType  |  イベントの種類。 これは、「メモリ アクセス」のすべての TTD です。メモリ オブジェクト。 |
| スレッド Id   |  OS スレッドは、要求を作成したスレッドの ID。 |
| UniqueThreadId |   トレースの間でのスレッドの一意の ID。 プロセスの有効期間にわたって正規スレッド Id を再利用を取得できますが、UniqueThreadIds ことはできません。 |
| TimeStart | A[位置オブジェクト](time-travel-debugging-position-objects.md)メモリへのアクセスが行われたときに、位置を記述します。 |
| 時刻終了 | A[位置オブジェクト](time-travel-debugging-position-objects.md)メモリへのアクセスが行われたときに、位置を記述します。 これは、常に TTD TimeStart と同じです。メモリ オブジェクト。
| AccessType |  アクセスの種類には、読み取り、書き込みまたはを実行します。 |
| IP         |  メモリ アクセスが行われたコードの命令ポインター。 |
| Address    |  読み取る/書き込む/実行アドレスの範囲内では、[beginAddress, endAddress) パラメーターから。Memory() します。  ハーフ オープンの間隔は、することに注意してください。  つまり、返されたイベントの中は endAddress に一致するアドレスが endAddress – 1 に一致するイベントが可能性があります。|
| サイズ       |  読み取り/書き込み/実行 (バイト単位) のサイズ。 これは、通常 8 バイト未満です。 コードの実行が発生した場合、実行された命令のバイト数になります。 |
| 値   | 読み取り、記述または実行された値。 実行の場合は、命令のコードのバイトが含まれます。 注命令のバイトは、逆アセンブラーによって、MSB の順序で並んでいるが、LSB 順序の値に格納されます。 |


## <a name="remarks"></a>注釈

次のアクセスの種類は、TTD で許可されます。メモリ クエリ:

-   r: 読み取り
-   w-書き込み
-   rw: 読み取り/書き込み
-   e-実行します。
-   rwe - 読み取り/書き込み/実行
-   ec - execute /change

この関数は関数を実行するときにかかるため、計算を行うことに注意してください。 


## <a name="example-usage"></a>使用例

この例では、グリッドの表示、トレースすべての位置を 0x00a4fca0 から始まるメモリの 4 バイトが読み取りアクセス権をどこまでの発生を示します。 メモリ アクセスの発生するたびにドリルダウンする任意のエントリをクリックします。

```dbgcmd
dx -g @$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")
```

![メモリ オブジェクト dx 例グリッド出力](images/ttd-time-travel-memory-object-dx-output.png) 

グリッド画面で、そのイベントの情報を表示するイベントのいずれかで TimeStart フィールドをクリックすることができます。 

```dbgcmd
0:000> dx -r1 @$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")[16].TimeStart
@$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")[16].TimeStart                 : 5D:113 [Time Travel]
    Sequence         : 0x5d
    Steps            : 0x113
```

トレース イベントが発生した位置に移動するには、[タイム トラベル] をクリックします。

```dbgcmd
0:000> dx @$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")[16].TimeStart.SeekTo()
@$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")[16].TimeStart.SeekTo()
(27b8.3168): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 5D:113

eax=0000004c ebx=00dd0000 ecx=00a4f89c edx=00a4f85c esi=00a4f89c edi=00b61046
eip=690795e5 esp=00a4f808 ebp=00a4f818 iopl=0         nv up ei pl nz na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000206
690795e5 ffb604040000    push    dword ptr [esi+404h] ds:002b:00a4fca0=00000000
```

この例には、すべてメモリ 0x1bf7d0 から始まる 4 バイトが読み取り/書き込みアクセスをどこまで、トレース内の位置の表示されます。 メモリ アクセスの発生するたびにドリルダウンする任意のエントリをクリックします。

```dbgcmd
0:000> dx @$cursession.TTD.Memory(0x1bf7d0,0x1bf7d4, "rw")
@$cursession.TTD.Memory(0x1bf7d0,0x1bf7d4, "rw")                
    [0x0]           
    [0x1]           
    [0x2]           
    [0x3]           
     ...
```
この例では次の項目の実行と変更アクセス 0x13a1710 から始まるメモリの 4 バイトのトレース内の位置をすべて表示されます。 メモリ アクセスのそれぞれについてドリルダウンを出現している箇所をクリックします。  

```dbgcmd
0:000> dx -r1 @$cursession.TTD.Memory(0x13a1710,0x13a1714, "ec")[0]
@$cursession.TTD.Memory(0x13a1710,0x13a1714, "ec")[0]                
    EventType        : MemoryAccess
    ThreadId         : 0x1278
    UniqueThreadId   : 0x2
    TimeStart        : 5B:4D [Time Travel]
    TimeEnd          : 5B:4D [Time Travel]
    AccessType       : Execute
    IP               : 0x13a1710
    Address          : 0x13a1710
    Size             : 0x1
    Value            : 0x55
```



## <a name="see-also"></a>関連項目

[タイム トラベル デバッグ - オブジェクトのタイム トラベルのデバッグの概要](time-travel-debugging-object-model.md)

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---


