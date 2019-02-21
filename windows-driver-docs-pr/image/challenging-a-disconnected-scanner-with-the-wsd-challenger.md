---
title: 切断されているスキャナー WSD 見据えて困難になります
description: 切断されているスキャナー WSD 見据えて困難になります
ms.assetid: f938a235-0360-43f9-9f84-6b9cb6ca9245
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0da63b43d71af20550fab340e97cc790ccdd6607
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558555"
---
# <a name="challenging-a-disconnected-scanner-with-the-wsd-challenger"></a>切断されているスキャナー WSD 見据えて困難になります

> [!IMPORTANT] 
> WSD 見据えて機能は非推奨とされているし、WSD の挑戦者に関連するすべてのドキュメントは、2018 年に削除されます。

Web サービス スキャナーのドライバーでは、スキャナーがオンラインに戻ったときに、デバイスとの通信を再確立するために切断されているスキャナーをチャレンジことができます。 ドライバーが WSD 見据えて DLL を使用すると、切断されているスキャナーの課題は、(*WSDCHNGR.DLL*) は、Windows Vista で提供されます。 Windows Image Acquisition (WIA) サービスも使用*WSDCHNGR.DLL*を積極的に WSDScan スキャナーのすべてのデバイスを監視し、通信が失敗するデバイスのチャレンジに応答するドライバーを有効にします。

デバイスのクラスの課題が開始した、 **WSDCHNGRChallengeDeviceClass** WSD チャレンジ関数。 WIA ドライバーでは、WIA サービス WIA のすべてのデバイスを呼び出すため、この関数を直接呼び出すする通常はありません。

ドライバーそのものが対応できない WIA ドライバーがサポートしているデバイスが切断されるとすぐにアンロード、ため*WSDCHNGR.DLL*読み込まれます。 そのため、ドライバーは、WSD 困難の監視を継続することはできませんし、オンラインに戻ったときに、デバイスに再接続することはできません。 代わりに、WIA ドライバーを使用してインストールされている、 *WSDScan.sys*カーネル モード ドライバーは、WIA サービスを使用して、デバイス クラスの挑戦する意欲やドライバーが読み込まれるを引き続き監視の困難を有効にします。

通常を使用して、WIA ドライバー *WSDScan.sys*次 WSD 見据えて関数のみを使用して。

<a href="" id="wsdchngrinitialize"></a>**WSDCHNGRInitialize**  
WIA ドライバー クライアントが使用する WSD 見据えてインターフェイスを初期化します。 ドライバーが読み込まれるときに、この関数を呼び出します。

<a href="" id="wsdchngrshutdown"></a>**WSDCHNGRShutdown**  
シャット ダウン、WSD 見据えてインターフェイス WIA ドライバーのクライアントを使用します。 ドライバーが読み込まれると、この関数を呼び出します。

**注**   WIA サービスが引き続き実行 WSD チャレンジの監視をデバイス ドライバーが読み込まれていないと、web サービスの課題のインターフェイスを終了した後、デバイスが WSDScan クラス デバイスの場合このシャット ダウンが発生したとき、.

 

<a href="" id="wsdchngrregisterdevicetochallenge"></a>**WSDCHNGRRegisterDeviceToChallenge**  
困難になることにデバイスを登録します。 ドライバーに潜在的な通信エラーが発生した後は、この関数を呼び出します。 チャレンジを複数回、同じデバイスを登録できます。 **WSDCHNGRRegisterDeviceToChallenge**返します S\_了解の最初のデバイスが正常に登録されている場合。 この関数は、秒を返します。\_困難になることに既に登録されているデバイスで呼び出された場合は FALSE。

次のコード例では、WSD チャレンジのこれらの関数を使用して、WSD 見据えてを初期化する方法と潜在的な通信障害の後を診断するため、スキャナーのデバイスを登録する方法を示します。

[エラー コードをフィルター処理するマクロの例](macro-example-to-filter-error-codes.md)

[切断された可能性のあるデバイスを診断するためのコード例](code-example-for-challenging-a-potentially-disconnected-device.md)

[ヘルパー メソッドを実装するためのコード例](code-example-for-implementing-helper-methods.md)

定義とこれらの例で使用されている変数の詳細については、次を参照してください。[定義と変数は、この例で使用](definitions-and-variables-used-in-the-examples.md)します。

 

 




