---
title: Windows 7 のシステム ファームウェアを構成し、Windows 10 を有効にします。
description: Windows 7 のシステム ファームウェアを構成し、Windows 10 を有効にします。
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7c604c75507c44c83ccf10afa43e27296affc6fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364585"
---
# <a name="configure-system-firmware-for-windows-7-and-enable-for-windows-10"></a>Windows 7 のシステム ファームウェアを構成し、Windows 10 を有効にします。


最新のシステム (Windows 7) などのダウンレベル オペレーティング システムのインストールをセットアップするには、Windows 7 と Windows 10 の両方の要件を満たすためにこのチェックリストを使用できます。

- UEFI 2.3.1 Errata C です。これは要件用に基づいて Windows 8.1、Windows 10 への今後のアップグレードに応じるためにします。

- Windows 10 のブート コンポーネントをセキュリティで保護された (証明書など) がインストールされています。参照してください[セキュア ブート](secure-boot.md)詳細についてはします。

- TPM 2.0 が Windows 7 での TPM のサポートのために使用します。 参照してください[KB2920188](https://support.microsoft.com/help/2920188/update-to-add-support-for-tpm-2-0-in-windows-7-and-windows-server-2008)詳細についてはします。

- システムとデバイス ファームウェアを更新できるは、モデル一意の ID を EFI システム リソース Table(ESRT) を代入するか。

- **UpdateCapsule()** と**QueryCapsuleCapabilitiesenabled()** UEFI でします。

- SMBIOS が構成され、設定ごと[SMBIOS](smbios.md)ガイダンス (妥当な範囲内のダウンレベル SMBIOS を使用する場合でも)。

- CSM が有効になっているとします。 これは、Windows 7 が必要ですし、セキュア ブートを無効になります。

- GPT ディスクとしてハード ドライブを構成します。

- デバイスの UEFI ブート用に構成します。

**注**これらの要件は、CSM の UEFI ブートを有効になっているなど、Windows 7 の要件と ESRT など、Windows 10 の要件の両方に基づいてと**UpdateCapsule()** 有効にしています。


