---
title: ドライバーの署名ポリシー
description: ドライバーの署名ポリシー
ms.assetid: c3ba672c-5bf2-4885-a85e-fa6d8a47ca54
keywords:
- ドライバー WDK、カーネル モード コードの署名ポリシーの署名
- ドライバー WDK、カーネル モード コードの署名ポリシーへの署名
- デジタル署名 WDK、カーネル モード コードの署名ポリシー
- WDK、カーネル モード コードの署名ポリシーの署名
- カーネル モード コードの署名ポリシー WDK
- カーネル モード ドライバーの WDK の署名
- ドライバー パッケージのデジタル署名 WDK
- パッケージのデジタル署名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c63e24a9c9d3bd2aee437b5275ada89686708a8c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346078"
---
# <a name="driver-signing-policy"></a>ドライバーの署名ポリシー

> [!NOTE]
> 以降では、Windows 10 version 1607 では、Windows はデベロッパー ポータルによって署名されていないの新しいカーネル モード ドライバーを読み込まれません。  署名済み、最初に、ドライバーを入手する[Windows ハードウェア デベロッパー センターのプログラムに登録](https://docs.microsoft.com/windows-hardware/drivers/dashboard/register-for-the-hardware-program)します。 なお、 [EV コード署名証明書](https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-a-code-signing-certificate)がダッシュ ボード アカウントを確立するために必要です。

ポータルにドライバーを提出する多くのさまざまな方法はあります。  実稼働ドライバーでは、以下に示すよう HLK/HCK テストのログを送信する必要があります。  Windows 10 クライアント システムにのみ、テストのために、ドライバーを送信できます[構成証明書の署名](../dashboard/attestation-signing-a-kernel-driver-for-public-release.md)、HLK テストは不要です。  または、テスト署名用にドライバーを送信するには、上の説明に従って、[新しいハードウェアの提出の作成](../dashboard/create-a-new-hardware-submission.md)ページ。

## <a name="exceptions"></a>例外

クロス署名されたドライバーは、次のいずれかに該当する場合にも許可されています。

* PC は、Windows 10 バージョン 1607 を Windows の以前のリリースからアップグレードされました。
* セキュア ブートは、bios がオフです。
* ドライバーは、サポートされているクロス署名 CA にチェーンされている年 7 月 29日 2015年より前に発行されたをエンド エンティティ証明書で署名されました。

詳細については、次を参照してください。[ドライバー署名の変更では、Windows 10 バージョン 1607](https://blogs.msdn.microsoft.com/windows_hardware_certification/2016/07/26/driver-signing-changes-in-windows-10-version-1607/)します。

## <a name="signing-a-driver-for-client-versions-of-windows"></a>Windows のクライアントのバージョンのドライバーの署名

Windows 10 用のドライバーをサインインさせる次の手順に従います。

1. 認定する Windows 10 の各バージョンでは、そのバージョンの Windows HLK (ハードウェア ラボ キット) をダウンロードし、そのバージョンのクライアントに対して証明書の完全なパスを実行します。 バージョンごとに 1 つのログが表示されます。
2. 複数のログがある場合は、最も新しい HLK を使用して 1 つのログにマージします。
3. ドライバーとマージされた HLK テスト結果を送信、 [Windows ハードウェア デベロッパー センター ダッシュ ボード ポータル](../dashboard/index.md)します。

バージョン固有の詳細を確認してください、 [WHCP (Windows ハードウェア互換性プログラム) ポリシー](https://docs.microsoft.com/windows-hardware/design/compatibility/whcp-specifications-policies)の対象とする Windows バージョン。

Windows 7、Windows 8、または Windows 8.1 ドライバーに署名するには、適切な HCK (ハードウェア認定キット) を使用します。  詳細については、次を参照してください。、 [Windows ハードウェア認定キット ユーザー ガイド](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))します。

## <a name="signing-a-driver-for-earlier-versions-of-windows"></a>Windows の以前のバージョンのドライバーの署名

Windows 10 バージョン 1607 を所有する前に、次の種類のドライバーには、クロス署名 Microsoft's クロス証明書と共に使用される Authenticode 証明書が必要です。

* カーネル モード デバイス ドライバー
* ユーザー モード デバイス ドライバー
* 保護されたコンテンツをストリームするドライバー。 保護されているユーザー モード Audio (PUMA) と保護されたオーディオのパス (PAP) を使用するオーディオ ドライバーやビデオ デバイス ドライバーを処理するには、ビデオ パス出力保護の管理 (PVP OPM) コマンドが保護されています。 詳細については、次を参照してください。[メディアの保護されているコンポーネントのコード署名](https://go.microsoft.com/fwlink/p/?linkid=74262)します。

## <a name="signing-requirements-by-version"></a>バージョン、署名の要件

クライアント オペレーティング システムのバージョンのポリシーの署名を次の表に示します。

セキュア ブートは、Windows Vista および Windows 7 に適用されないことに注意してください。

|適用対象:|Windows Vista、Windows 7 です。Windows 8 + セキュア ブートをオフ|Windows 8、Windows 8.1、Windows 10 バージョン 1507 と 1511 セキュア ブートで|Windows 10 バージョン 1607 + セキュア ブートで|
|--- |--- |--- |--- |
|**アーキテクチャ:**|64 ビットのみの 32 ビットに必要な署名なし|64 ビット、32 ビット|64 ビット、32 ビット|
|**必要な署名:**|埋め込みまたはカタログ ファイル|埋め込みまたはカタログ ファイル|埋め込みまたはカタログ ファイル|
|**署名アルゴリズム:**|SHA1|SHA1|SHA2 または SHA1|
|**証明書:**|コードの整合性によって信頼されている標準のルート|コードの整合性によって信頼されている標準のルート|Microsoft ルート機関 2010、Microsoft ルート証明機関では、Microsoft ルート機関|

ドライバー コードの署名、だけでなく、PnP デバイス インストールの署名のドライバーをインストールするための要件を満たす必要があります。  詳細については、次を参照してください。[プラグ アンド プレイ (PnP) デバイスのインストール要件を署名](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)します。

ELAM ドライバーの署名方法の詳細については、次を参照してください。[早期起動マルウェア対策](https://msdn.microsoft.com/library/windows/desktop/hh848061(v=vs.85).aspx)します。

## <a name="see-also"></a>関連項目

* [開発およびテスト時に、未署名のドライバ パッケージをインストールします。](installing-an-unsigned-driver-during-development-and-test.md)
* [ドライバーのパブリック リリースへの署名](signing-drivers-for-public-release--windows-vista-and-later-.md)
* [開発およびテスト中にドライバーへの署名](signing-drivers-during-development-and-test.md)
* [デジタル署名](driver-signing.md)
* [インストールおよび署名されたドライバー パッケージを使用した負荷の問題のトラブルシューティング](troubleshooting-install-and-load-problems-with-signed-driver-packages.md)
