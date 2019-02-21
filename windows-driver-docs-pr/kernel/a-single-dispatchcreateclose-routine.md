---
title: 1 つの DispatchCreateClose ルーチン
description: 1 つの DispatchCreateClose ルーチン
ms.assetid: 6127d696-2409-49fc-9cbd-ba1b13c0c672
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchCreateClose ルーチン
- DispatchCreateClose ルーチン
- Irp_mj_create 用 I/O 関数のコード
- 未完了の I/O 関数のコード
- ディスパッチ ルーチン WDK カーネルを作成します。
- ディスパッチ ルーチン WDK カーネルを閉じる
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a89e0e96edb174d3fa2c041f0b6f05f994c2a3f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536296"
---
# <a name="a-single-dispatchcreateclose-routine"></a>1 つの DispatchCreateClose ルーチン





多くのドライバーのチェーン内の下位レベルでは特にドライバーはドライバーを階層化、だけでの受信時にその存在を確立する必要があります、*作成*要求し、の受信を確認するだけで必要があります、 *を閉じる*要求。

たとえば、ポート用のドライバー デバイス コント ローラーを呼び出す 1 つまたは複数の密接に結合されたクラスのドライバーと[ **IoGetDeviceObjectPointer** ](https://msdn.microsoft.com/library/windows/hardware/ff549198)を最小限に抑える必要があります[ *DispatchCreateClose* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 ルーチンがあります何も複数の完全な IRP とおり。

```cpp
    :    : 
{ 
    Irp->IoStatus.Status = STATUS_SUCCESS; 
 Irp->IoStatus.Information = 0; 
    IoCompleteRequest(Irp, IO_NO_INCREMENT); 
 return STATUS_SUCCESS; 
}
```

この最小*DispatchCreateClose*日常的なセット、**情報**; 作成要求が開かれたファイル オブジェクトを示すゼロ、I/O 状態ブロックのメンバー**情報**終了要求の意味を持ちません。 日常的なセット、**状態**ステータス メンバー\_ドライバーが I/O を受け入れ可能であることを示す、この状態値が要求の成功とも返します。

この最小*DispatchCreateClose*ルーチンの IRP の発信者の優先度を上げることがなく IRP の作成が完了すると (IO\_いいえ\_インクリメント)、発信元が待機すると見なされますので、要求が完了するが、不確定な非常に小さい間隔です。

作業量を*DispatchCreateClose*ルーチンがの一部は、ドライバーのデバイスまたは基になるデバイスの性質と、ドライバーの設計で部分的に依存します。 ドライバーは、非常にさまざまな操作の作成と閉じる要求を実行する場合にこれらの要求を処理するよう[DispatchCreate および DispatchClose ルーチンを分離](separate-dispatchcreate-and-dispatchclose-routines.md)します。

論理または物理デバイスを表すファイル オブジェクトを開くための作成要求を処理するには、最上位レベルのドライバーが、以下を実行します。

1.  呼び出す[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174) IRP では、I/O スタックの場所にポインターを取得します。

2.  確認**FileObject**.**ファイル名**、I/O スタックの場所と状態が IRP の完了\_成功の場合は、Unicode の文字列で**FileName**長さは 0 それ以外の場合、状態が IRP を完了\_。無効な\_パラメーター。

前の手順に従って、デバイス上の pseudofile を開こうとしてできます問題が発生するありません後ようにします。 これにより、存在しない開こうとすると、たとえば、 \\\\デバイス\\parallel0\\temp.dat します。

 

 




