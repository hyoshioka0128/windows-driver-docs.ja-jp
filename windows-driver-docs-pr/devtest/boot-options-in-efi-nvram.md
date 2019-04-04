---
title: EFI NVRAM にブート オプション
description: NVRAM のファームウェア ストア ブート オプションを拡張ファームウェア インターフェイス (EFI) を持つコンピューターは、コンピューターをオフにする場合でも、状態が保持されます。
ms.assetid: 99247d03-1723-4a2b-8ef4-c1f39687642f
keywords:
- NVRAM ブート オプション WDK
- EFI NVRAM ブート オプション WDK
- ブート オプション WDK、EFI NVRAM
- 拡張ファームウェア インターフェイスの WDK ブート オプション
- Itanium プロセッサ ブート オプション WDK
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: abeb2d396114f1e244215f200846eeb9ecdf5602
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560003"
---
# <a name="boot-options-in-efi-nvram"></a>EFI NVRAM にブート オプション


> [!IMPORTANT] 
> このトピックでは、Windows XP および Windows Server 2003 でサポートされるブート オプションについて説明します。 Windows の最新バージョンのブート オプションを変更する場合は、[Windows Vista 以降のブート オプション](boot-options-in-windows-vista-and-later.md)を参照してください。

拡張ファームウェア インターフェイス (EFI) のファームウェア、Intel Itanium 2 プロセッサなどのコンピューターでは、NVRAM、編集できますが、コンピューターをオフにする場合でも、その状態を保持するストレージ メディアでブート オプションを格納します。 EFI ファームウェアが BIOS ファームウェア、として同じ目的を果たしますが、従来の BIOS の多くの制限を克服します。 X86 ベースのシステムで BIOS およびブート マネージャー (NTLDR) で実装されるスタートアップ関数は、EFI コンポーネント、つまり、EFI の BIOS と EFI ブート マネージャによって処理されます。

ドライバーのデバッグと Windows XP、Windows Server 2003、およびその先行タスクを実行している (EFI) ベースのシステム テストに関連する機能を構成するには、NVRAM にブート オプションを編集する必要があります。 次のセクションでは、簡単な EFI NVRAM にブート オプションについて説明し、ブート オプションは、このテクノロジを使用するシステムに固有の側面について説明します。

Windows Vista および Windows の以降のバージョンでは、BIOS および EFI ベースのコンピューター上のブート オプションが格納されている*ブート構成データ*(BCD)、ブート オプションのファームウェアに依存しない構成と記憶域システム。 詳細については、[Windows Vista 以降のブート オプション](boot-options-in-windows-vista-and-later.md)を参照してください。

Itanium ベース システムのブート オプションの詳細については、拡張ファームウェア インターフェイスの仕様を参照してください。 更新された仕様のコピーをダウンロードすることができます、 [Intel Extensible Firmware Interface](https://go.microsoft.com/fwlink/p/?linkid=10596) web サイト。

このセクションの内容:

- [Efi ブート オプションの概要](overview-of-boot-options-in-efi.md)
- [Efi ブート オプションの編集](editing-boot-options-in-efi.md)
- [Efi ブート オプションをバックアップします。](backing-up-boot-options-in-efi.md)
