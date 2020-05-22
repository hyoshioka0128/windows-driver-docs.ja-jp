---
title: EFI NVRAM でのブート オプション
description: 拡張ファームウェアインターフェイス (EFI) ファームウェアが搭載されたコンピューターは、ブートオプションを NVRAM に格納しますが、コンピューターの電源をオフにしても状態を保持します。
ms.assetid: 99247d03-1723-4a2b-8ef4-c1f39687642f
keywords:
- NVRAM ブートオプション WDK
- EFI NVRAM ブートオプション WDK
- ブートオプション WDK、EFI NVRAM
- 拡張ファームウェアインターフェイスの WDK ブートオプション
- Itanium プロセッサブートオプション WDK
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: a57af80def6935acf594b7123282cffd6b64acd9
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769684"
---
# <a name="boot-options-in-efi-nvram"></a>EFI NVRAM でのブート オプション


> [!IMPORTANT] 
> このトピックでは、Windows XP と Windows Server 2003 でサポートされているブートオプションについて説明します。 Windows の最新バージョンのブートオプションを変更する場合は、「 [windows のブートオプション](boot-options-in-windows.md)」を参照してください。

Intel Itanium 2 プロセッサなど、拡張ファームウェアインターフェイス (EFI) ファームウェアを搭載したコンピューターでは、ブートオプションが NVRAM に格納されます。この記憶域メディアは編集できますが、コンピューターの電源をオフにしても状態を保持します。 EFI ファームウェアは BIOS ファームウェアと同じ目的で機能しますが、従来の BIOS の多くの制限を克服します。 X86 ベースシステムの BIOS およびブートマネージャー (NTLDR) で実装されるスタートアップ関数は、efi コンポーネント、つまり efi BIOS と EFI ブートマネージャーによって処理されます。

Windows XP、Windows Server 2003、およびその前に実行されている EFI ベースのシステムでのドライバーのデバッグとテストに関連する機能を構成するには、NVRAM でブートオプションを編集する必要があります。 以下のセクションでは、EFI NVRAM のブートオプションについて簡単に説明し、このテクノロジを使用するシステムに固有のブートオプションの側面について説明します。

Windows Vista 以降のバージョンの Windows では、BIOS ベースおよび EFI ベースのコンピューターのブートオプションは*ブート構成データ*(BCD) に格納されます。これは、ブートオプション用のファームウェアに依存しない構成および記憶域システムです。 詳細については、「 [Windows Vista 以降のブートオプション](boot-options-in-windows-vista-and-later.md)」を参照してください。

Itanium ベースシステムでのブートオプションの詳細については、「拡張ファームウェアインターフェイスの仕様」を参照してください。 更新された仕様のコピーは、 [Intel 拡張ファームウェアインターフェイス](https://www.intel.com/content/www/us/en/architecture-and-technology/unified-extensible-firmware-interface/efi-homepage-general-technology.html)の web サイトからダウンロードできます。

ここでは、以下の内容について説明します。

- [EFI でのブート オプションの概要](overview-of-boot-options-in-efi.md)
- [EFI でのブート オプションの編集](editing-boot-options-in-efi.md)
- [EFI でのブート オプションのバックアップ](backing-up-boot-options-in-efi.md)
