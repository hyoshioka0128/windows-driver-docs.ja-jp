---
title: Preparsed データを取得します。
description: Preparsed データを取得します。
ms.assetid: 7a2bdbd1-a970-421f-bbaa-40fe589bb49a
keywords:
- WDK を非表示に preparsed データ コレクション
- HID コレクション WDK、preparsed データ
- WDK の HID preparsed データ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 089101113e7099787f7d36d760cc79fb96ced77a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559585"
---
# <a name="obtaining-preparsed-data"></a>Preparsed データを取得します。





このセクションでは、ユーザー モード アプリケーションとカーネル モード ドライバーの HID のコレクションを取得する方法について説明します[preparsed データ](preparsed-data.md)、を非表示レポートには、コレクションを記述するための非透過構造体。

### <a name="user-mode-application"></a>ユーザー モード アプリケーション

ユーザー モード アプリケーションは、のいずれかを呼び出す前に、コレクションの preparsed データを取得する必要があります、 [HIDClass サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff538865)preparsed データを必要とします。 アプリケーションは、デバイス上の開いているファイルがある限り、コレクションの preparsed データへのアクセスを保持する必要があります。

アプリケーションを呼び出すと、HID コレクション上のファイルを開いたら、 [ **HidD\_GetPreparsedData** ](https://msdn.microsoft.com/library/windows/hardware/ff539679)コレクションを返すルーチンに割り当てられたバッファー内のデータを preparsed します。

アプリケーションを呼び出す必要があります[ **HidD\_FreePreparsedData** ](https://msdn.microsoft.com/library/windows/hardware/ff538893)アプリケーションが不要になったコレクションへのアクセスを必要とします。

### <a name="kernel-mode-driver"></a>カーネル モード ドライバー

ドライバーにコレクションの取得、カーネル モード ドライバーでは、HID コレクションが開いたら、 [preparsed データ](preparsed-data.md)次のようにします。

-   コレクションの preparsed データの長さを取得します。

-   コレクションの preparsed データを取得します。

Preparsed データの長さを確認するドライバーを使用して、 [ **IOCTL\_HID\_取得\_コレクション\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff541092)要求。 この要求を返します、 [ **HID\_コレクション\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff539870)構造体。 **DescriptorSize**この構造体のメンバーは、コレクションの preparsed データのバイト単位でサイズを指定します。 ドライバーは、少なくともこの非ページ プールからバッファーを割り当てる必要があります preparsed データを保持するサイズ。

Preparsed データ バッファーを割り当てた後、ドライバーを使用して、 [ **IOCTL\_HID\_取得\_コレクション\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff541089)への要求preparsed データを取得します。

Preparsed データを入手すると、ドライバーと共に使用できます、 **HidP\_**<em>Xxx</em> HID サポート ルーチン HID コレクションの機能に関する情報を取得し、抽出するにはHID レポートからデータを制御します。

 

 




