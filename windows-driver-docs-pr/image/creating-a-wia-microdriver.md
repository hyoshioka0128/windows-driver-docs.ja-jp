---
title: WIA Microdriver を作成します。
description: WIA Microdriver を作成します。
ms.assetid: 4f453569-d768-47fb-9b70-ebb51e303cf0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f77d905d77de2217b7fde09f510771391e70a92
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535902"
---
# <a name="creating-a-wia-microdriver"></a>WIA Microdriver を作成します。





多くのフラット ベッド スキャナーは、同様の方法で制御されます。 Microsoft 提供の一般的なドライバーの中、WIA ベッド ドライバーと呼ばれるモデルの間で共通の動作が抽出されています。 このドライバーは、必要なデバイスに固有の動作を実装する検索プログラムのベンダによって提供される、microdriver と呼ばれる、DLL を呼び出します。 と共に、microdriver WIA ベッド ドライバーは、WIA ミニドライバーとして使用できます。 Microdriver を使用する利点は、実装し、デバッグが非常に簡単であります。 すべてスキャナーは、microdriver によってサポートできます。 単純なデバイスに最も適しています (なし、両面印刷ユニットまたはその他の機能の詳細に設定)、基本機能ドライバーが必要な場合またはします。

**注**  このセクションで説明されている、WIA microdrivers、WIA 1.0。 現在 WIA 2.0 用の対応する WIA microdriver モデルではありません。 WIA 2.0 をサポートする Windows のバージョンがコンピューターで実行する WIA microdriver を開発するかどうか (Windows Vista またはそれ以降)、この WIA microdriver WIA 1.0 デバイスと同様に機能は、互換性モードが WIA 1.0 WIA 2.0 アプリケーションで使用されます。

 

次の図は、WIA microdriver アーキテクチャのコンポーネントを示します。

![wia microdriver アーキテクチャのコンポーネントを示す図](images/art-6.png)

WIA ベッド ドライバーは、microdriver WIA microdriver 関数を呼び出すことによって、WIA サービスからの要求を処理します。 Microdriver には、これらの各関数を実装する必要があります。 A [ **SCANINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff547361)通信スキャン ウィンドウ解像度などのスキャンのパラメーターを格納および microdriver に構造体が渡されます。 WIA ベッド ドライバーは SCANINFO 構造体の値を読み取りますが、それらを書き込むことはありません。 SCANINFO メンバーを設定する microdriver の役目です。

Microdriver は、スキャンのすべてのパラメーターを格納する必要がありますに格納されている値に依存する必要があります、 [ **SCANINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff547361)構造体。 これは、デバイスに複数のアプリケーション アクセスをサポートするために重要です。 2 つのアプリケーションは、同時に、同じデバイスでのスキャンを設定する場合を実行している microdriver の 1 つだけのコピー。 このような状況では、microdriver はアプリケーションがデバイスにアクセスしようとに応じて異なる SCANINFO 構造体が 2 つのいずれかで呼び出されます。

 

 




