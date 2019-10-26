---
title: TTD Memory オブジェクト
description: このセクションでは、タイムトラベルデバッグに関連付けられているメモリモデルオブジェクトについて説明します。
ms.date: 01/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6b960859d1698518e451b555e0fce385af3bfac6
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916190"
---
# <a name="ttd-memory-objects"></a>TTD Memory オブジェクト

## <a name="description"></a>説明
*TTD memory*は、Beginaddress、endaddress、および dataAccessMask パラメーターを受け取り、メモリアクセス情報を含むメモリオブジェクトのコレクションを返すメソッドです。

## <a name="parameters"></a>パラメーター

| プロパティ | 説明 |
| --- | --- |
| beginAddress | 0x で始まるメモリオブジェクトの開始アドレス。|
| endAddress| 0x で始まるメモリオブジェクトの終了アドレス。|
| dataAccessMask |二重引用符で囲まれたデータアクセスマスク。 読み取りの場合は r、書き込みの場合は e、execute の場合は e、変更の場合は c を指定できます。 |


## <a name="children"></a>Children

| オブジェクト      | 説明 |
| ----------- | ----------- |
| EventType  |  イベントの種類。 これは、すべての TTD の "MemoryAccess" です。メモリオブジェクト。 |
| スレッド Id   |  要求を行ったスレッドの OS スレッド ID。 |
| UniqueThreadId |   トレース全体のスレッドの一意の ID。 通常のスレッド Id は、プロセスの有効期間にわたって再利用できますが、UniqueThreadIds することはできません。 |
| TimeStart | メモリアクセスが行われたときの位置を記述する[位置オブジェクト](time-travel-debugging-position-objects.md)。 |
| TimeEnd | メモリアクセスが行われたときの位置を記述する[位置オブジェクト](time-travel-debugging-position-objects.md)。 これは、常に TTD の TimeStart と同じです。メモリオブジェクト。
| AccessType |  アクセスの種類 (読み取り、書き込み、または実行)。 |
| IP         |  メモリアクセスを行ったコードの命令ポインター。 |
| Address    |  読み取り/書き込み/実行されたアドレスであり、パラメーターの [beginAddress, endAddress) の範囲内にあります。メモリ ()。  間隔はハーフオープンであることに注意してください。  つまり、返されたイベントのいずれにも endAddress に一致するアドレスはありますが、endAddress –1と一致するイベントが存在する可能性があります。|
| Size       |  読み取り/書き込み/実行のサイズ (バイト単位)。 通常、これは8バイト以下です。 コード実行の場合、これは実行された命令のバイト数です。 |
| Value   | 読み取り、書き込み、または実行された値。 実行の場合は、命令のコードバイトが含まれます。 命令バイトは逆アセンブラーによって MSB 順序で一覧表示されますが、値には LSB 順序で格納されることに注意してください。 |


## <a name="remarks"></a>注釈

TTD では、次のアクセスの種類を使用できます。メモリクエリ:

-   r-読み取り
-   w-書き込み
-   rw-読み取り/書き込み
-   e-実行
-   rwe-読み取り/書き込み/実行
-   ec-/change を実行する

これは計算を実行する関数であるため、実行には時間がかかります。 


## <a name="example-usage"></a>使用例

この例では、トレース内のすべての位置をグリッドで表示しています。これは、0x00a4fca0 で始まる4バイトのメモリが読み取りアクセスであったことを示しています。 任意のエントリをクリックすると、メモリアクセスが発生するたびにドリルダウンされます。

```dbgcmd
dx -g @$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")
```

![メモリオブジェクト dx のサンプルグリッドの出力](images/ttd-time-travel-memory-object-dx-output.png) 

グリッド表示のいずれかのイベントで TimeStart フィールドをクリックすると、そのイベントに関する情報が表示されます。 

```dbgcmd
0:000> dx -r1 @$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")[16].TimeStart
@$cursession.TTD.Memory(0x00a4fca0,0x00a4fca4, "r")[16].TimeStart                 : 5D:113 [Time Travel]
    Sequence         : 0x5d
    Steps            : 0x113
```

イベントが発生したトレース内の位置に移動するには、[タイムトラベル] をクリックします。

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

この例では、0x1bf7d0 で始まる4バイトのメモリを持つトレース内のすべての位置が、読み取り/書き込みにアクセスされたことが示されています。 任意のエントリをクリックすると、メモリアクセスが発生するたびにドリルダウンされます。

```dbgcmd
0:000> dx @$cursession.TTD.Memory(0x1bf7d0,0x1bf7d4, "rw")
@$cursession.TTD.Memory(0x1bf7d0,0x1bf7d4, "rw")                
    [0x0]           
    [0x1]           
    [0x2]           
    [0x3]           
     ...
```
この例では、0x13a1710 で始まる4バイトのメモリが実行され、変更がアクセスされたトレースのすべての poアッドが一覧表示されています。 任意の項目をクリックしてドリルダウンすると、メモリアクセスの各発生に関する追加情報が表示されます。  

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

## <a name="see-also"></a>参照

[タイムトラベルデバッグ-タイムトラベルデバッグオブジェクトの概要](time-travel-debugging-object-model.md)

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)

