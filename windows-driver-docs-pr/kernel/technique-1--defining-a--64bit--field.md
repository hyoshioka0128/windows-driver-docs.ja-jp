---
title: 手法「64 ビット」フィールドを定義する 1
description: ドライバーの「64 ビット」フィールドを定義します。
ms.assetid: 6498e66c-145e-4f7e-a065-cbd781e142cc
keywords:
- 32 ビットの I/O をサポートして WDK 64 ビット、64 ビット フィールドの定義
- 64 ビット フィールドには、WDK のカーネルが定義されています。
- WDK の 64 ビットのビット フィールド
- WDK の 64 ビットの個別の制御コード
- 制御コード WDK 64 ビット
- WDK の 64 ビットのコードをファイル システムの制御
- FSCTL WDK 64 ビット
- I/O 制御コード WDK カーネル、64 ビット ドライバーで 32 ビットの I/O
- Ioctl WDK カーネルでは、64 ビット ドライバーで 32 ビットの I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cd78bd2a9304cd6cfe3732189fc00828d43b17f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345538"
---
# <a name="technique-1-defining-a-64bit-field"></a>方法 1: 「64 ビット」フィールドを定義します。





「64 ビット」フィールドは、IOCTL に FSCTL をコントロールのコードで定義されます。 このフィールドには、常に 64 ビットの呼び出し元の設定が、32 ビットのチェック ボックスをオフは常にいる、ビット フラグが含まれています。 「64 ビット」フィールドは、ドライバー固有ですが、32 ビットの呼び出し元には設定されませんを少しする必要があります、コントロールのコードでどのビットが選択されます。 ほとんどのドライバーに最適では、関数のフィールドの最上位ビット (MSB) です。

たとえば、32 ビット ドライバーで使用される IOCTL (FSCTL) コントロールのコードには、4 つのビット フィールドが含まれています。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>デバイスの種類</th>
<th>アクセス権</th>
<th>関数</th>
<th>メソッド</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>16 ビット</p></td>
<td><p>2 つのビット</p></td>
<td><p>12 ビット</p></td>
<td><p>2 つのビット</p></td>
</tr>
</tbody>
</table>

 

関数のフィールドで、MSB を設定、既存のドライバーの定義済みの制御コードのいずれもいれば、これらの制御コードは、32 ビット ユーザー モード アプリケーションで使用する続行できます。

64 ビットの呼び出し元を対応するためには、ドライバーは、1 つのビットで短い関数フィールドを定義します。 このビットが「64 ビット」フィールドとして再定義します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>デバイスの種類</th>
<th>アクセス権</th>
<th>64 ビット</th>
<th>関数</th>
<th>メソッド</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>16 ビット</p></td>
<td><p>2 つのビット</p></td>
<td><p>1 ビット</p></td>
<td><p>11 ビット</p></td>
<td><p>2 つのビット</p></td>
</tr>
</tbody>
</table>

 

次のコード例では、ドライバーのヘッダー ファイルで「64 ビット」フィールドを定義する方法を示します。

```cpp
#define REGISTER_FUNCTION 0     // Define the IOCTL function code

#ifdef  _WIN64
#define CLIENT_64BIT   0x800
#define REGISTER_FUNCTION 0
#define IOCTL_REGISTER   CTL_CODE(FILE_DEVICE_UNKNOWN, \
  CLIENT_64BIT|REGISTER_FUNCTION, METHOD_BUFFERED, FILE_ANY_ACCESS)
#else
#define IOCTL_REGISTER   CTL_CODE(FILE_DEVICE_UNKNOWN, \
  REGISTER_FUNCTION, METHOD_BUFFERED, FILE_ANY_ACCESS)
#endif

typedef struct _IOCTL_PARAMETERS {
    PVOID   Addr;
    SIZE_T  Length;
    HANDLE  Handle;
} IOCTL_PARAMETERS, *PIOCTL_PARAMETERS;
```

 

 




