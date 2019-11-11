---
title: ドライバー署名ポリシー
description: ドライバー署名ポリシー
ms.assetid: c3ba672c-5bf2-4885-a85e-fa6d8a47ca54
keywords:
- ドライバー署名 WDK、カーネルモードコード署名ポリシー
- 署名ドライバー WDK、カーネルモードコード署名ポリシー
- デジタル署名 WDK、カーネルモードコード署名ポリシー
- 署名 WDK、カーネルモードコード署名ポリシー
- カーネルモードコード署名ポリシー WDK
- カーネルモードドライバー署名 WDK
- ドライバーパッケージのデジタル署名 WDK
- パッケージデジタル署名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfee7045135387e53438ea53119ac75dad8c9e8b
ms.sourcegitcommit: 15217d1d11a4d43048ff42e5aa3b7f37da7f28ff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753873"
---
# <a name="driver-signing-policy"></a>ドライバー署名ポリシー

> [!NOTE]
> Windows 10 バージョン1607以降では、開発者ポータルによって署名されていない新しいカーネルモードドライバーは読み込まれません。  ドライバーが署名されるようにするには、最初に[Windows Hardware Dev Center プログラムに登録](https://docs.microsoft.com/windows-hardware/drivers/dashboard/register-for-the-hardware-program)します。 ダッシュボードアカウントを確立するには、 [EV コード署名証明書](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-a-code-signing-certificate)が必要であることに注意してください。

ポータルにドライバーを送信するには、さまざまな方法があります。  実稼働ドライバーの場合は、以下の説明に従って HLK/HCK テストログを送信する必要があります。  Windows 10 クライアント専用システムでのテストでは、HLK テストを必要としない、[構成証明の署名](../dashboard/attestation-signing-a-kernel-driver-for-public-release.md)用のドライバーを送信できます。  または、「[新しいハードウェアの送信を作成する](../dashboard/create-a-new-hardware-submission.md)」ページの説明に従って、テスト署名用のドライバーを送信することもできます。

## <a name="exceptions"></a>例外

次のいずれかに該当する場合、クロス署名ドライバーは引き続き許可されます。

* PC は、以前のリリースの Windows から Windows 10 バージョン1607にアップグレードされました。
* BIOS でセキュアブートがオフになっています。
* ドライバーは、サポートされているクロス署名 CA にチェーンされている2015年7月29日より前に発行されたエンドエンティティ証明書で署名されています。

システムが正常に起動しないようにするために、ブートドライバーはブロックされませんが、プログラム互換性アシスタントによって削除されます。

## <a name="signing-a-driver-for-client-versions-of-windows"></a>Windows のクライアントバージョンのドライバーに署名する

Windows 10 のドライバーに署名するには、次の手順を実行します。

1. 認定を受けたい Windows 10 のバージョンごとに、そのバージョンの Windows HLK (ハードウェアラボキット) をダウンロードし、そのバージョンのクライアントに対して完全な証明書パスを実行します。 バージョンごとに1つのログが取得されます。
2. 複数のログがある場合は、最新の HLK を使用して1つのログにマージします。
3. ドライバーとマージされた HLK テスト結果を[Windows Hardware Developer Center ダッシュボードポータル](../dashboard/index.md)に送信します。

バージョン固有の詳細については、対象とする Windows バージョンの[Whcp (Windows ハードウェア互換性プログラム) ポリシー](https://docs.microsoft.com/windows-hardware/design/compatibility/whcp-specifications-policies)を確認してください。

Windows 7、Windows 8、または Windows 8.1 のドライバーに署名するには、適切な HCK (ハードウェア認定キット) を使用します。  詳細については、『 [Windows ハードウェア認定キットユーザーズガイド』](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))を参照してください。

## <a name="signing-a-driver-for-earlier-versions-of-windows"></a>以前のバージョンの Windows のドライバーに署名する

Windows 10 バージョン1607より前では、次の種類のドライバーでは、クロス署名のために Microsoft のクロス証明書と共に使用される Authenticode 証明書が必要です。

* カーネルモードデバイスドライバー
* ユーザーモードデバイスドライバー
* 保護されたコンテンツをストリーミングするドライバー。 これには、保護されたユーザーモードのオーディオ (PUMA) と保護されたオーディオパス (PAP) を使用するオーディオドライバー、および保護されたビデオパスを処理するビデオデバイスドライバー (PVP-OPM) が含まれます。 詳細については、「[保護されたメディアコンポーネントのコード署名](https://go.microsoft.com/fwlink/p/?linkid=74262)」を参照してください。

## <a name="signing-requirements-by-version"></a>バージョン別の署名要件

次の表は、クライアントオペレーティングシステムのバージョンの署名ポリシーを示しています。

セキュアブートは Windows Vista および Windows 7 には適用されないことに注意してください。

|適用対象:|Windows Vista、Windows 7、Windows 8 以降 (セキュアブートオフ)|Windows 8、Windows 8.1、Windows 10、バージョン1507、1511 (セキュアブートオン)|Windows 10、バージョン1607、1703、1709 (セキュアブートオン)|Windows 10、バージョン 1803 + セキュアブートオン|
|--- |--- |--- |--- |--- |
|**アーキテクチャ**|64ビットのみ、32ビットに署名は必要ありません|64-bit、32ビット|64-bit、32ビット|64-bit、32ビット|
|**署名が必要:**|埋め込みファイルまたはカタログファイル|埋め込みファイルまたはカタログファイル|埋め込みファイルまたはカタログファイル|埋め込みファイルまたはカタログファイル|
|**署名アルゴリズム:**|SHA2|SHA2|SHA2|SHA2|
|**証明**|コードの整合性によって信頼されている標準のルート|コードの整合性によって信頼されている標準のルート|Microsoft ルート機関2010、microsoft ルート証明機関、microsoft ルート機関|Microsoft ルート機関2010、microsoft ルート証明機関、microsoft ルート機関|

ドライバーコード署名に加えて、ドライバーをインストールするための PnP デバイスインストール署名の要件を満たす必要もあります。  詳細については、「[プラグアンドプレイ (PnP) デバイスのインストール署名の要件](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)」を参照してください。

ELAM ドライバーの署名の詳細については、「[早期起動マルウェア対策](https://docs.microsoft.com/windows/desktop/w8cookbook/secured-boot)」を参照してください。

## <a name="see-also"></a>参照

* [開発およびテスト中の署名されていないドライバーパッケージのインストール](installing-an-unsigned-driver-during-development-and-test.md)
* [パブリックリリースのドライバーに署名する](signing-drivers-for-public-release--windows-vista-and-later-.md)
* [開発およびテスト中のドライバーへの署名](signing-drivers-during-development-and-test.md)
* [デジタル署名](driver-signing.md)
* [署名されたドライバーパッケージのインストールおよび読み込みに関する問題のトラブルシューティング](troubleshooting-install-and-load-problems-with-signed-driver-packages.md)
