---
title: NX プールの互換性の問題
description: NX を使用すると Windows 8 用のドライバー バイナリ内の非ページ プールは、Windows の以前のバージョンでこれらのバイナリを実行する場合の互換性の問題が検索されます。
ms.assetid: 652AE9A2-D733-4EC2-9D49-B95DDABE42B1
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 67a23d8b593d0bcd944e187980ef25e7f021cc07
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365420"
---
# <a name="nx-pool-compatibility-issues"></a>NX プールの互換性の問題


NX を使用すると Windows 8 用のドライバー バイナリ内の非ページ プールは、Windows の以前のバージョンでこれらのバイナリを実行する場合の互換性の問題が検索されます。

Windows 8、NX をサポートするために Windows の最初のバージョンは、非ページ プール。 ただし、多数の既存のカーネル モード ドライバーのバイナリは、Windows 7 および x86、x64、および IA64 プロセッサのアーキテクチャ上で実行される Windows の以前のバージョンで使用できます。 非ページ メモリを割り当て、これらのドライバーを使用して、実行可能ファイルの非ページ プール代わりに、NX 非ページ プール。 旧バージョンと互換性のため、Windows 7、および、Windows の以前のバージョンで実行して、非ページ プールからメモリを割り当てるカーネル モード ドライバーのバイナリは、変更しなくても Windows 8 で実行されます。 ただし、これらのドライバーは活用できません NX の可用性を Windows 8 での非ページ プール。

## <a name="running-existing-driver-binaries-on-windows8"></a>Windows 8 上の既存のドライバー バイナリが実行中


ドライバーのバイナリは、Windows 7 (または可能性があります、Windows の以前のバージョン) をビルドしたし、使用する、 **NonPagedPool**プールの種類、Windows 8 での実行が妨げられていません。 旧バージョンとの互換性を有効にする、 **NonPagedPoolExecute**として同じ値を持つ定数が定義されている、 **NonPagedPool**の定数、 [**プール\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_pool_type)列挙体。 したがって、このドライバーを実行する Windows のすべてのバージョンでは、非ページ プールから、ドライバーによって割り当てられるメモリは常に実行可能ファイル。

Windows 8 は、ARM アーキテクチャをサポートするために Windows の最初のバージョンです。 したがって、用のドライバー バイナリ ARM Windows の以前のバージョンに組み込まれているし、旧バージョンと互換性が必要なはありません。 指定する ARM で Windows 用に作成されたすべてのドライバーが代わりに、予想される**NonPagedPoolNx**の代わりに**NonPagedPoolExecute**での非ページ プールの割り当ての実行可能ファイルを明示的に要求しない限りメモリ。

ドライバーは x86、x64、または IA64 から ARM に移植した場合、[プール\_NX\_OPTIN\_自動](multiple-binary-opt-in-pool-nx-optin-auto.md)オプトイン メカニズムは、ドライバーのビルド プロセス中に自動的に適用されます。 このオプトイン メカニズムのすべてのインスタンスを既定では、置換するプリプロセッサを使用して、 **NonPagedPool**定数名を**NonPagedPoolNx**します。 必要に応じてを使って、[プール\_NX\_OPTOUT](selective-opt-out-pool-nx-optout.md)オプトアウト メカニズムを上書きするファイルごとにこのオプトイン メカニズム。

## <a name="other-compatibility-issues"></a>その他の互換性の問題


**NonPagedPoolNx**プールの種類が Windows 8 以降でサポートされています。 Windows の以前のバージョンのドライバーでこのプールの種類を使用しないでください。 プール アロケーターは、Windows の以前のバージョンで正常に動作しないドライバーを使用し、割り当てが要求したとき、 **NonPagedPoolNx**プールの種類。

Windows 8 では、前に Windows のバージョンでは、 **NonPagedPoolExecute**の代わりに、プールの種類を自由に使用できる、 **NonPagedPool**プールの種類。 [**プール\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_pool_type)列挙体を定義**NonPagedPool**と**NonPagedPoolExecute**に同じ値を指定します。

## <a name="nx-pool-type-porting-guidelines"></a>NX プール型の移植のガイドライン


サポートを追加するいくつかの方法がある Windows 8 または Windows の以前のバージョンから後でドライバー コードを移植するときに、 **NonPagedPoolNx**と**NonPagedPoolExecute**プール種類。 次の一覧から、お客様の要件に最適なアプローチを選択します。

-   ほとんどまたはすべてのインスタンスを置き換える場合は、ドライバーは、Windows 8 より前のバージョンの Windows で実行するものではありません、 **NonPagedPool**で**NonPagedPoolNx**します。 ほとんど置き換える必要があります、開発者のインスタンスのみ**NonPagedPool**で**NonPagedPoolExecute します。**

-   ドライバーのソース コードは、Windows 8 および Windows での以前のバージョンの両方を対象バージョンごとのバイナリの別のドライバーを配布する場合は、プールを使用して\_NX\_OPTIN\_自動オプトイン メカニズム。 インスタンスは、この方法で必要ありません**NonPagedPool**でドライバーのソース。 詳細については、次を参照してください。[プール オプトイン メカニズムに NX](nx-pool-opt-in-mechanisms.md)します。

-   ドライバーのソース コードが Windows 8 および Windows での以前のバージョンの両方を対象とサポートされているすべてのバージョンで実行する二項 1 つのドライバーを配布する場合は、プールを使用して\_NX\_OPTIN オプトイン メカニズム。 インスタンスは、この方法で必要ありません**NonPagedPool**でドライバーのソース。 詳細については、次を参照してください。[プール オプトイン メカニズムに NX](nx-pool-opt-in-mechanisms.md)します。

これら 3 つのアプローチのいずれかは、ほとんどのドライバーを迅速かつ簡単に移植できます。

すべてのインスタンスが単純に上書きされない**NonPagedPool**ドライバー コードの**NonPagedPoolExecute**します。 使用して、 **NonPagedPoolExecute**プールのみ実行可能にする必要があるプールの割り当ての種類 (たとえば、コードを実行する - just-in-time で、または、JIT によって生成コンパイラ)。

 

 




