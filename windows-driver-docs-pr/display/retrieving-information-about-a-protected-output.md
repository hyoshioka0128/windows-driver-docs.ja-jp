---
title: 保護されている出力に関する情報を取得します。
description: 保護されている出力に関する情報を取得します。
ms.assetid: 20e268b8-fea0-48dd-a3cd-3cbb4233ef99
keywords:
- OPM WDK の表示、保護対象を取得する情報の出力
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47cd647618525bf90a3e809ad763a91f0f1f4d98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532876"
---
# <a name="retrieving-information-about-a-protected-output"></a>保護されている出力に関する情報を取得します。


ディスプレイのミニポート ドライバーでは、グラフィックス アダプターの物理出力コネクタに関連付けられている保護された出力に関する情報を取得する要求を受信できます。 ディスプレイのミニポート ドライバーの[ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725)関数へのポインターを渡される、 [ **DXGKMDT\_OPM\_GET\_情報\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff560868)構造体、*パラメーター*情報の要求を含むパラメーター。 *DxgkDdiOPMGetInformation*に必要な情報を書き込みます、 [ **DXGKMDT\_OPM\_要求された\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560910)構造体、*RequestedInformation*パラメーターを指します。 **GuidInformation**と**abParameters** DXGKMDT のメンバー\_OPM\_取得\_情報\_パラメーターは、情報の要求を指定します。 情報の要求に応じて、ディスプレイのミニポート ドライバーがのメンバーを設定する必要があります、 [ **DXGKMDT\_OPM\_標準\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560925)、 [**DXGKMDT\_OPM\_出力\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff560890)、または[ **DXGKMDT\_OPM\_実際\_出力\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff560840)で必要な情報とポイント構造、 **abRequestedInformation** DXGKMDT のメンバー\_OPM\_要求された\_については、その構造にします。 ドライバーを指定した後、 **cbRequestedInformationSize** (たとえば、sizeof (DXGKMDT\_OPM\_標準\_情報)) と**abRequestedInformation**DXGKMDT のメンバー\_OPM\_要求された\_については、ドライバーは、1 つのキー暗号化ブロック チェーン (CBC) を計算する必要があります-DXGKMDT 内のデータのメッセージ認証コード (OMAC) モード\_OPM\_要求された\_情報この OMAC を設定する必要があります、 **omac** DXGKMDT のメンバー\_OPM\_要求された\_情報。 OMAC の計算の詳細については、次を参照してください。、 [OMAC 1 アルゴリズム](https://go.microsoft.com/fwlink/p/?linkid=70417)します。

**注**  する前に[ **DxgkDdiOPMGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559725)返します、ディスプレイのミニポート ドライバーは、ことを確認する必要がありますで指定されている OMAC、 **omac**のメンバー [ **DXGKMDT\_OPM\_取得\_情報\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff560868)が正しい。 ドライバーを確認する必要がありますも、シーケンス番号で指定された、 **ulSequenceNumber** DXGKMDT のメンバー\_OPM\_取得\_情報\_パラメーターに一致するシーケンスドライバーが格納されている数。 ドライバーでは、ストアドのシーケンス番号を増やす必要がありますから。

 

**注**  ドライバーでは、128 ビットの暗号強度が高いランダムな数値を返す必要があります、 **rnRandomNumber** DXGKMDT のメンバー\_OPM\_標準\_については、 [ **DXGKMDT\_OPM\_出力\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff560890)、または DXGKMDT\_OPM\_実際\_出力\_形式。 ランダムな番号、送信元アプリケーションによって生成され、記載されて、 **rnRandomNumber** DXGKMDT のメンバー\_OPM\_取得\_情報\_パラメーター。

 

ドライバーには、指定された要求の次の情報が返されます。

-   DXGKMDT の\_OPM\_取得\_サポートされている\_保護\_型に設定、 **guidInformation**メンバーで定義されていないと、 **abParameters** 、DXGKMDT のメンバー\_OPM\_取得\_情報\_パラメーター構造体、ドライバーを使用できる保護メカニズムの種類を示します。 使用可能な保護の種類を示すために、ドライバーがからの値の有効なビットごとの OR 組み合わせを返します、 [ **DXGKMDT\_OPM\_保護\_型**](https://msdn.microsoft.com/library/windows/hardware/ff560898)内の列挙型、 **ulInformation** DXGKMDT のメンバー\_OPM\_標準\_情報。 DXGKMDT\_OPM\_保護\_型\_HDCP や DXGKMDT\_OPM\_保護\_型\_DPCP 値は無効です。

-   DXGKMDT の\_OPM\_取得\_コネクタ\_型を設定**guidInformation**で定義されていないと**abParameters**ドライバーを示します、コネクタ タイプです。 コネクタの種類を示すために、ドライバーが値の有効なビットごとの OR 組み合わせを返します、 [ **D3DKMDT\_ビデオ\_出力\_テクノロジ**](https://msdn.microsoft.com/library/windows/hardware/ff546605)内の列挙型、 **ulInformation** DXGKMDT のメンバー\_OPM\_標準\_情報。

-   DXGKMDT の\_OPM\_取得\_仮想\_保護\_レベルまたは DXGKMDT\_OPM\_取得\_実際\_保護\_レベルの設定**guidInformation**で保護の種類を設定および**abParameters**、ドライバーの保護レベル値を返します、 **ulInformation**メンバーの[ **DXGKMDT\_OPM\_標準\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560925)します。 保護の種類が DXGKMDT 場合\_OPM\_保護\_型\_HDCP からの保護レベル値は、 [ **DXGKMDT\_OPM\_HDCP\_保護\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff560878)列挙体。 保護の種類が DXGKMDT 場合\_OPM\_保護\_型\_DPCP からの保護レベル値は、 [ **DXGKMDT\_OPM\_DPCP\_保護\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff560861)列挙体。

    DXGKMDT\_OPM\_取得\_仮想\_保護\_レベルの要求で返す現在設定されている保護された出力の保護レベル。 DXGKMDT\_OPM\_取得\_実際\_保護\_レベルの要求で返す現在設定されている保護された出力に関連付けられている物理コネクタの保護レベル。

-   DXGKMDT の\_OPM\_取得\_アダプター\_BUS\_型を設定**guidInformation**で定義されていないと**abParameters**、ドライバー母マザーボード チップセットの north ブリッジにグラフィックス アダプターを接続するバスの実装の種類を識別します。 型とバスの実装を特定するには、ドライバーはから値の有効なビットごとの OR 組み合わせを返します、 [ **DXGKMDT\_OPM\_BUS\_型\_AND\_ 。実装**](https://msdn.microsoft.com/library/windows/hardware/ff560841)で列挙、 **ulInformation** DXGKMDT のメンバー\_OPM\_標準\_情報。

-   DXGKMDT の\_OPM\_取得\_現在\_HDCP\_SRM\_にバージョン設定**guidInformation**で定義されていないと**abParameters**、ドライバーの値を返します、 **ulInformation**のメンバー [ **DXGKMDT\_OPM\_標準\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560925)バージョン番号の現在高帯域幅デジタル コンテンツの保護 (HDCP) システム Renewability メッセージ (SRM) の保護された出力を識別します。 最下位ビット (ビット 0 ~ 15) には、リトル エンディアン形式で SRM のバージョン番号が含まれます。 SRM バージョン番号の詳細については、次を参照してください。、 [HDCP 仕様のリビジョン 1.1](https://go.microsoft.com/fwlink/p/?linkid=38728)します。

-   DXGKMDT の\_OPM\_取得\_実際\_出力\_形式の設定**guidInformation**で定義されていないと**abParameters**、ドライバーがのメンバーの情報を返します[ **DXGKMDT\_OPM\_実際\_出力\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff560840)を記述する方法保護された出力に関連付けられている物理コネクタを通過したシグナルは、書式設定されます。

-   DXGKMDT の\_OPM\_取得\_出力\_ID で設定**guidInformation**で定義されていないと**abParameters**ドライバーには、情報が返されます、。メンバーの[ **DXGKMDT\_OPM\_出力\_ID** ](https://msdn.microsoft.com/library/windows/hardware/ff560890)出力コネクタを識別します。

-   DXGKMDT の\_OPM\_取得\_DVI\_特性の設定、 **guidInformation**メンバーで定義されていないと、 **abParameters**のメンバー、DXGKMDT\_OPM\_取得\_情報\_電気の特性をデジタル ビデオ インターフェイス (DVI) のコネクタの出力パラメーター構造体ドライバーを示します。 DVI 電気的特性を示すために、ドライバーからの値のいずれかを返します、 [ **DXGKDT\_OPM\_DVI\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff560819)内の列挙型**ulInformation**のメンバー [ **DXGKMDT\_OPM\_標準\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560925)します。

 

 





