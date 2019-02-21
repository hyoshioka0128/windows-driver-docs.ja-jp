---
title: プリンター インターフェイス Dll の概要
description: プリンター インターフェイス Dll の概要
ms.assetid: 1993d818-9761-418e-96c3-e3c46965bef1
keywords:
- プリンター インターフェイス DLL の詳細については、プリンター インターフェイス DLL の WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d6f65a96b58a4557f128d52727c6e70ace6149c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530055"
---
# <a name="introduction-to-printer-interface-dlls"></a>プリンター インターフェイス Dll の概要





プリンターは、通常、ユーザーが印刷されるドキュメントごとに変更できる変更可能な構成オプションの数が多いを提供します。 画像の解像度、サイズ、色、および、と共に、用紙、用紙トレイおよびフォントの選択などのオプションは、アプリケーションで呼び出すことができるユーザー インターフェイスを介してアクセス可能である必要があります。

プリンター ドライバーの*プリンター インターフェイス DLL*プリンターの構成オプションのユーザー インターフェイスをエクスポートするための担当ユーザー モードで実行します。 このインターフェイスを提供する必要があります[プリンターのプロパティ シートのページを作成する](creating-property-sheet-pages-for-printers.md)します。 (印刷フォルダー) などのアプリケーションは、印刷スプーラーによってエクスポートされる Win32 関数を呼び出すことによって、インターフェイスを表示し、スプーラーはさらに、呼び出す[プリンター インターフェイス Dll によって定義されている関数](functions-defined-by-printer-interface-dlls.md)します。

構成オプションのユーザー インターフェイスを提供することは、プリンター インターフェイス DLL の唯一の責任ではありません。 DLL は、ドライバーのインストールとアップグレード、またはプリンターの追加と接続などのシステムの印刷関連イベントのドライバーに通知する、スプーラーを呼び出すことができる関数をエクスポートします。

 

 




