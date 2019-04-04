---
title: 保護されている出力の COPP と互換性のある情報の取得
description: ディスプレイのミニポート ドライバーでは、グラフィックス アダプターの物理出力コネクタに関連付けられている保護された出力に関する COPP と互換性のある情報を取得する要求を受信できます。
ms.assetid: 9114f232-4123-47a8-b43d-62d14b9f6b08
keywords:
- OPM WDK の表示、COPP と互換性のある情報を取得します。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 3d8a6c83ae7aa46153de12437537a871fee99661
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530430"
---
# <a name="retrieving-copp-compatible-information-on-protected-output"></a>保護されている出力の COPP と互換性のある情報の取得


ディスプレイのミニポート ドライバーでは、グラフィックス アダプターの物理出力コネクタに関連付けられている保護された出力に関する COPP と互換性のある情報を取得する要求を受信できます。 ディスプレイのミニポート ドライバーの[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)関数へのポインターを渡される、 [ **DXGKMDT\_OPM\_COPP\_互換性のある\_取得\_情報\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff560859)構造体、*パラメーター*パラメーターが含まれていますが、情報の要求。 *DxgkDdiOPMGetCOPPCompatibleInformation*に必要な情報を書き込みます、 [ **DXGKMDT\_OPM\_要求された\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560910)構造体、 *RequestedInformation*パラメーターを指します。 **GuidInformation**と**abParameters** DXGKMDT のメンバー\_OPM\_COPP\_互換性のある\_取得\_情報\_パラメーターは、情報の要求を指定します。 情報の要求に応じて、ディスプレイのミニポート ドライバーがのメンバーを設定する必要があります、 [ **DXGKMDT\_OPM\_標準\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560925)、 [**DXGKMDT\_OPM\_実際\_出力\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff560840)、 [ **DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_シグナリング**](https://msdn.microsoft.com/library/windows/hardware/ff560830)、または[ **DXGKMDT\_OPM\_接続\_HDCP\_デバイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560854)で必要な情報とポイント構造、 **abRequestedInformation** DXGKMDT のメンバー\_OPM\_要求された\_については、その構造にします。 ドライバーを指定した後、 **cbRequestedInformationSize** (たとえば、 <strong>sizeof (</strong>DXGKMDT\_OPM\_標準\_情報<strong>)</strong>) と**abRequestedInformation** DXGKMDT のメンバー\_OPM\_要求された\_については、ドライバーは、1 つのキー暗号化ブロック チェーン (CBC) を計算する必要があります-DXGKMDT 内のデータのメッセージ認証コード (OMAC) モード\_OPM\_要求された\_情報この OMAC を設定する必要があります、 **omac** DXGKMDT のメンバー\_OPM\_要求された\_情報。 OMAC の計算の詳細については、、 [OMAC 1 アルゴリズム](https://go.microsoft.com/fwlink/p/?linkid=70417)を参照してください。

**注**  する前に[ **DxgkDdiOPMGetCOPPCompatibleInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559720)戻り値は、ディスプレイのミニポート ドライバーを確認する必要があります、で指定されたシーケンス番号**ulSequenceNumber** DXGKMDT のメンバー\_OPM\_COPP\_互換性のある\_取得\_情報\_パラメーターと一致するシーケンス番号をドライバーが格納されています。 ドライバーでは、ストアドのシーケンス番号を増やす必要がありますから。

 

**注**  ドライバーでは、128 ビットの暗号強度が高いランダムな数値を返す必要があります、 **rnRandomNumber** DXGKMDT のメンバー\_OPM\_標準\_情報、DXGKMDT\_OPM\_実際\_出力\_形式、DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_シグナル型、または DXGKMDT\_OPM\_接続\_HDCP\_デバイス\_情報。 ランダムな番号、送信元アプリケーションによって生成され、記載されて、 **rnRandomNumber** DXGKMDT のメンバー\_OPM\_COPP\_互換性のある\_取得\_情報\_パラメーター。

 

ドライバーには、指定された要求の次の情報が返されます。

-   DXGKMDT の\_OPM\_取得\_サポートされている\_保護\_型に設定、 **guidInformation**メンバーで定義されていないと、 **abParameters** DXGKMDT のメンバー\_OPM\_COPP\_互換性のある\_取得\_情報\_パラメーター、ドライバーが保護メカニズムの使用可能な型を示します。 使用可能な保護の種類を示すために、ドライバーがからの値の有効なビットごとの OR 組み合わせを返します、 [ **DXGKMDT\_OPM\_保護\_型**](https://msdn.microsoft.com/library/windows/hardware/ff560898)内の列挙型、 **ulInformation** DXGKMDT のメンバー\_OPM\_標準\_情報。 DXGKMDT\_OPM\_保護\_型\_ACP、DXGKMDT\_OPM\_保護\_型\_CGMSA、および DXGKMDT\_OPM\_保護\_型\_COPP\_互換性のある\_HDCP 値は無効です。

-   DXGKMDT の\_OPM\_取得\_コネクタ\_型を設定**guidInformation**で定義されていないと**abParameters**ドライバーを示します、コネクタ タイプです。 コネクタの種類を示すために、ドライバーが値の有効なビットごとの OR 組み合わせを返します、 [ **D3DKMDT\_ビデオ\_出力\_テクノロジ**](https://msdn.microsoft.com/library/windows/hardware/ff546605)内の列挙型、 **ulInformation** DXGKMDT のメンバー\_OPM\_標準\_情報。

-   DXGKMDT の\_OPM\_取得\_仮想\_保護\_レベルまたは DXGKMDT\_OPM\_取得\_実際\_保護\_レベルの設定**guidInformation**で保護の種類を設定および**abParameters**、ドライバーの保護レベル値を返します、 **ulInformation**メンバーの[ **DXGKMDT\_OPM\_標準\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560925)します。 保護の種類が DXGKMDT 場合\_OPM\_保護\_型\_から ACP では、保護レベル値は、 [ **DXGKMDT\_OPM\_ACP\_保護\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff560834)列挙体。 保護の種類が DXGKMDT 場合\_OPM\_保護\_型\_CGMSA からの保護レベル値は、 [ **DXGKMDT\_OPM\_CGMSA**](https://msdn.microsoft.com/library/windows/hardware/ff560846)列挙体。 保護の種類が DXGKMDT 場合\_OPM\_保護\_型\_COPP\_互換性のある\_HDCP からの保護レベル値は、 [ **DXGKMDT\_OPM\_HDCP\_保護\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff560878)列挙体。

    DXGKMDT\_OPM\_取得\_仮想\_保護\_レベルの要求で返す現在設定されている保護された出力の保護レベル。 DXGKMDT\_OPM\_取得\_実際\_保護\_レベルの要求で返す現在設定されている保護された出力に関連付けられている物理コネクタの保護レベル。

-   DXGKMDT の\_OPM\_取得\_アダプター\_BUS\_型を設定**guidInformation**で定義されていないと**abParameters**、ドライバー母マザーボード チップセットの north ブリッジにグラフィックス アダプターを接続するバスの種類を識別します。 バスの種類を識別するために、ドライバーが値の有効なビットごとの OR 組み合わせを返します、 [ **DXGKMDT\_OPM\_BUS\_型\_AND\_実装** ](https://msdn.microsoft.com/library/windows/hardware/ff560841)で列挙、 **ulInformation** DXGKMDT のメンバー\_OPM\_標準\_情報。

    ドライバーでは、DXGKMDT を組み合わせることができますのみ\_OPM\_COPP\_互換性のある\_BUS\_型\_インターフェイスがない場合は、バスの種類値のいずれかで (0x80000000) を統合型の値グラフィックス アダプターとその他のサブシステムの間の信号、公開されている仕様と標準コネクタの種類を使用する拡張バスで利用できます。 メモリ バスは、この定義から除外されます。

-   DXGKMDT の\_OPM\_取得\_実際\_出力\_形式の設定**guidInformation**で定義されていないと**abParameters**、ドライバーがのメンバーの情報を返します[ **DXGKMDT\_OPM\_実際\_出力\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff560840)を記述する方法保護された出力に関連付けられている物理コネクタを通過したシグナルは、書式設定されます。

-   DXGKMDT の\_OPM\_取得\_ACP\_AND\_CGMSA\_設定シグナル通知**guidInformation**で定義されていないと**abParameters**、ドライバーがのメンバーの情報を返します[ **DXGKMDT\_OPM\_ACP\_AND\_CGMSA\_シグナリング**](https://msdn.microsoft.com/library/windows/hardware/ff560830)保護された出力に関連付けられている物理コネクタを経由する信号を保護する方法を説明します。

-   DXGKMDT の\_OPM\_取得\_接続\_HDCP\_デバイス\_における**guidInformation**で定義されていないと**abParameters**、ドライバーがのメンバーの情報を返します[ **DXGKMDT\_OPM\_接続\_HDCP\_デバイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff560854)高帯域幅デジタル コンテンツの保護 (HDCP) 情報が含まれています。

 

 





