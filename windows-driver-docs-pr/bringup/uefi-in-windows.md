---
title: Windows の UEFI
description: Windows の UEFI
ms.assetid: 14b54fe3-49f7-4ad8-b9b6-ecc747dff137
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5365356f82c31d87d170819ff5d7183c7c453ebc
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652758"
---
# <a name="uefi-in-windows"></a>Windows の UEFI


**注**  このセクションの一部の情報は、Windows 10 Mobile と特定のプロセッサアーキテクチャにのみ適用される場合があります。

 

Windows では、SoC ファームウェアのブートローダーから OS へのシステム制御のハンドオフをサポートするために、Unified Extensible Firmware Interface (UEFI) を利用しています。 UEFI 環境は、Windows デバイスが起動され、OS が実行される最小ブート OS です。

UEFI は標準的な UEFI 仕様に基づくブートローダー用の一般的なフレームワークであり、標準的な環境と、オペレーティングシステムの起動を可能にするプラットフォームファームウェアのインターフェイスのセットを記述します。 UEFI 仕様は[https://uefi.org/specifications](https://go.microsoft.com/fwlink/p/?LinkId=218221)で入手できます。 UEFI の非常に低いレベルの性質のため、それぞれの実装は特定の SoC に固有です。 Windows デバイスの場合、主要な UEFI 環境と一部の UEFI ドライバーが SoC ベンダーによって提供されます。 追加の UEFI ドライバーと UEFI アプリケーション (フラッシュされたアプリケーションなど) は、Microsoft によって提供されます。

UEFI 仕様に記載されている実装の詳細に加えて、SoC プラットフォームで Windows を実行するための UEFI 要件が追加されています。 これらの要件については、「 [Windows 上の Windows の UEFI の最小要件](minimum-uefi-requirements-for-windows-on-soc-platforms.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="minimum-uefi-requirements-for-windows-on-soc-platforms.md" data-raw-source="[Minimum UEFI requirements for Windows on SoC platforms](minimum-uefi-requirements-for-windows-on-soc-platforms.md)">SoC プラットフォーム上の Windows の最小 UEFI 要件</a></p></td>
<td><p>Unified Extensible Firmware Interface (UEFI) は、Windows を実行している SoC プラットフォームに必要なブートファームウェアです。 このセクションでは、SoC プラットフォームで Windows を実行するための UEFI 実装要件について説明します。 これらの要件に対する監視と準拠は、Windows の適切な機能を保証するのに役立ちます。</p></td>
</tr>
<tr class="even">
<td><p><a href="uefi-protocols-for-windows.md" data-raw-source="[UEFI protocols for Windows](uefi-protocols-for-windows.md)">Windows 用 UEFI プロトコル</a></p></td>
<td><p>このセクションでは、Windows で定義されている UEFI プロトコルについて説明します。 これらのプロトコルは、UEFI 仕様で定義されているプロトコルによって拡張され、ブートプロセス中に特定の機能を実行するために Windows によって使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="windows-uefi-firmware-update-platform.md" data-raw-source="[Windows UEFI firmware update platform](windows-uefi-firmware-update-platform.md)">Windows UEFI ファームウェア更新プラットフォーム</a></p></td>
<td><p>Windows は、UEFI UpdateCapsule 機能を使用して処理されるドライバーパッケージを使用して、システムとデバイスのファームウェアの更新プログラムをインストールするためのプラットフォームをサポートしています。 このプラットフォームにより、一貫性のある信頼性の高いファームウェア更新エクスペリエンスが提供され、エンドユーザーにとって重要なシステムファームウェア更新プログラムの発見可能性が向上します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="uefi-components-for-windows"></a>Windows 用 UEFI コンポーネント


次の図は、Windows デバイスの主要な UEFI コンポーネントを示しています。

![windows phone 用 uefi コンポーネント](images/oem-uefi-components.png)

## <a name="oem-components-in-the-uefi-environment"></a>UEFI 環境の OEM コンポーネント


Oem は、デバイスの製造とサービスの提供を支援する UEFI アプリケーションを追加できます。 エンドユーザーがこれらのアプリケーションにアクセスできないようにする必要があります。 エンドユーザー向けの UEFI アプリケーションは、Microsoft によってのみ実装され、Windows ブートマネージャーによって起動されます。

UEFI アプリケーションを実装することを選択した Oem は、可能な限りメモリフットプリントが小さく、起動時間に影響を与えないようにする必要があります。 UEFI 環境用のコンポーネントの作成の詳細については、SoC ベンダーに問い合わせてください。

**重要**   oem は、特定のハードウェアに対応するために、SoC ベンダーから提供されている特定の UEFI ドライバーを置き換える必要がある場合もあります。 詳細については、SoC ベンダに関する説明を参照してください。

 

## <a name="related-topics"></a>関連トピック
[Windows 用 UEFI プロトコル](uefi-protocols-for-windows.md)  



