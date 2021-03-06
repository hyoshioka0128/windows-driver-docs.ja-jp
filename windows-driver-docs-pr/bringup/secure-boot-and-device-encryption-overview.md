---
title: セキュリティで保護されたブートとデバイス暗号化の概要
description: このトピックでは、セキュリティで保護された boot デバイス暗号化機能と、OEM の主な要件と考慮事項に重点を置いての概要を示します。
ms.assetid: 4e206bd2-7bb4-48c2-9e01-8da041e798ef
ms.date: 05/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07e484a77f8b3686b17b3bfb750d15cd2470577e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364518"
---
# <a name="secure-boot-and-device-encryption-overview"></a>セキュリティで保護されたブートとデバイス暗号化の概要


このトピックでは、セキュリティで保護された boot デバイス暗号化機能と、OEM の主な要件と考慮事項に重点を置いての概要を示します。

**適用対象**

- Windows 10 Mobile

## <a name="secure-boot"></a>セキュア ブート


セキュア ブートは、実行を許可する前に、デバイスのファームウェア イメージを検証するプロセスです。 以降の (製造中にファームウェアでプロビジョニングされているキーのハッシュで構成される) の信頼のルートでは、セキュリティで保護された boot 暗号によって検証、UEFI 環境に、プレ UEFI ブート ローダーからのすべてのブート コンポーネントのデジタル署名し、最後に、メインの OS とすべてのコンポーネントをで実行されること (ドライバーやアプリの場合)。 セキュア ブートは、承認済みのコードは、オペレーティング システムの読み込み前に実行できることを確認するのに役立ちます。

SoC ベンダーによって提供されるコア UEFI 環境では、UEFI 仕様のセクション 27 で説明した UEFI セキュア ブートの標準を実装します。 この標準では、すべてが UEFI では、それらが実行される前に UEFI ランタイム変数にプロビジョニングされたキーに対してドライバーとアプリケーションを検証します。 プロセスについて説明します。 SoC ベンダーによって実装されるコア UEFI 環境に関する詳細については、次を参照してください。[ブートおよび UEFI](boot-and-uefi.md)と[Windows での UEFI](uefi-in-windows.md)します。

### <a name="secure-boot-process"></a>セキュリティで保護された起動プロセス

次の図は、セキュリティで保護された起動プロセスの概要を示します。

![セキュア ブート フロー](images/oem-secureboot-flow.png)

次の手順では、このプロセスの詳細について説明します。

1.  セキュア ブートを有効にするのには、Oem は、セキュア ブート キーのプロビジョニング、さまざまなヒューズを倒すなど、製造時に、一連のタスクを実行します。

2.  信頼のルートに対して事前 UEFI ブート ローダーの署名を検証するプロセスを開始するデバイスを起動します。 このチェックが成功した場合、UEFI ブート マネージャーは読み込まれます。

3.  UEFI ブート マネージャーには、各 UEFI アプリまたはドライバーが読み込まれたら、バイナリを適切に署名を確認します。 任意のコンポーネントのチェックに失敗した場合は、コンポーネントが読み込まれていないし、ブート プロセスは失敗します。

4.  ブート マネージャー (Microsoft によって提供される UEFI コンポーネント) が正常に読み込まれると、BCD (ブート構成データ) の特定の設定はそのままことを確認します。 Windows 10 がセキュア ブートのポリシーが正しいと判断し、others.o を無視します。 値を使用してそのままいない場合

5.  ブート マネージャーでは、ブート ローダーの署名を検証し、署名が有効な場合にのみ、ブート ローダーを読み込みます。

6.  ブート ローダーは、それらとカーネルを読み込む前に、すべての起動に不可欠なドライバーの署名を検証します。 この時点では、読み込む前にすべてのドライバーとアプリの署名を検証する、カーネルの責任になります。

### <a name="oem-requirements-and-considerations"></a>OEM の要件と考慮事項

Oem は、次の要件とセキュア ブートに関連する考慮事項の注意する必要があります。

-   セキュア ブート、セキュア ブート キーのプロビジョニング、さまざまな JTAG ヒューズを倒すなどを有効にする製造時に、一連のタスクを実行する必要があります。

-   Oem は、最低限のハードウェア要件仕様で、少なくとも 512 KB RPMB パーティションを持つ、eMMC 部分を使用する必要があります。

-   製造時に、セキュア ブートの有効化プロセスの一環として、リプレイ保護されたメモリ ブロック (RPMB) eMMC 部分をプロビジョニングする必要があります。 このプロビジョニングの発生後特定 eMMC 部分と、デバイスで SoC コンポーネントをまとめて; バインドします。eMMC 部分は削除され、OS、RPMB の利用を持つ別のデバイスで再利用されることはできません。

-   セキュア ブートを有効にすると、すべてのドライバーとデバイス上のアプリは、ために、オペレーティング システムによって読み込まれる署名する必要があります。 詳細については、次を参照してください。[コード署名](https://docs.microsoft.com/previous-versions/windows/hardware/code-signing/dn756634(v=vs.85))します。

## <a name="device-encryption"></a>デバイスの暗号化


BitLocker テクノロジを使用して内部データのパーティションにローカルに格納されているすべてのユーザー データを暗号化する Windows 10 Mobile をサポートします。 これにより、ハードウェアのオフライン攻撃からローカル デバイス データの機密性を保護します。 デバイスが紛失または盗難にあった場合、およびユーザーが PIN を使って、デバイスをロックしている場合は、デバイスの暗号化により、攻撃者がデバイスから機密情報を回復することは難しいことができます。

デバイスの暗号化が有効になっている場合は、メインの OS とデータ ストアの内部ユーザーのパーティションが暗号化されます。 SD カード、電話に挿入するには暗号化されません。

ユーザーが有効にまたはデバイスの暗号化を使用して、デバイスをオフにする**設定** = &gt; **システム** = &gt; **デバイスの暗号化**電子メールは、デバイスと同期されなくなど、デバイスのコンプライアンスとコンプライアンスに問題のトリガーを解除を配置この可能性があります。 デバイスの暗号化が有効の場合は、デバイスをセキュリティで保護する際に PIN を作成する、ユーザーが求められます。

### <a name="oem-requirements-and-considerations"></a>OEM の要件と考慮事項

次の要件とデバイスの暗号化に関連する考慮事項に注意する必要があります。

-   既定では、デバイスの暗号化が有効になっていません。 デバイスの暗号化は、次のシナリオで自動的に有効にします。

    -   ユーザーは、Microsoft Exchange server、接続デバイスの暗号化を必要とするように構成して、デバイスに、Outlook アカウントを追加します。

    -   ユーザーがアプリの会社にデバイスを接続し、アカウントにエンタープライズ デバイス管理サーバーがデバイスの暗号化を必要とするデバイスにポリシーをプッシュします。

    これらのシナリオでは、デバイスの暗号化ポリシーの変更は、デバイスで構成した後、メインの OS とデータ ストアの内部ユーザーのパーティションを暗号化をデバイスは自動的に開始します。 デバイスの暗号化作業は、エンドユーザーに影響を最小限に調整されます。

-   OEM の有効化タスクがデバイスの暗号化に固有ではありません。 ただし、Oem は、セキュア ブートを有効にする手順に従う必要があります。

-   デバイスでデバイスの暗号化を有効にした後、メインの OS (たとえば、UEFI にケア アプリを顧客するなど) の外部で実行されるアプリは、デバイスでデータを暗号化されたパーティションに書き込むことはできません。 メインの OS または OS 更新プログラムでのアプリだけでは、暗号化されたパーティションにデータを記述できます。

 

 




