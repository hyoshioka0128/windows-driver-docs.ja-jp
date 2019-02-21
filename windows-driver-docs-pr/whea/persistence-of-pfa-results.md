---
title: PFA 結果の永続化
description: PFA 結果の永続化
ms.assetid: de79b87e-2c9a-4181-b531-8ad283bb9d5b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7290a26106ccdaee47377040ff17592d345b3e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553794"
---
# <a name="persistence-of-pfa-results"></a>PFA 結果の永続化


エラー修正コード (ECC) がメモリ ページが失敗する可能性が現在 PFA レジストリ設定、PFA ストアに基づくことを予測的な障害の分析 (PFA) が予測されるたびに (または*が解決しない*) メモリ ページのページのフレーム数 (PFN). PFA 内のリストに PFN を保持する、 **{badmemory}** ブート構成データ (BCD) のシステム ストアのオブジェクト。 この一覧には、PFNs、PFA が失敗する可能性を予測するすべてのメモリ ページが含まれています。 Windows オペレーティング システムが起動されるたびに、システムによって使用されているからこのリスト内のメモリ ページを除外します。

**注**  物理メモリの PFN を特定の物理メモリ モジュールにマップするための標準的な業界はありません。 したがって、WHEA では、メモリ モジュールの失敗に関する情報を提供できません。

 

Windows では、このリスト、BCD システム ストアからをクリアするための自動化されたメカニズムは提供されません。 ときに、障害が発生したシステム メモリが置き換えられると、システム管理者は、BCDEdit のコマンド ライン ツールを使用して、この一覧を手動で消去する必要があります。 一覧は消去されませんが、Windows が引き続き、システムで使用されてから、リスト内のメモリ ページを除外する場合でも問題のあるメモリ モジュールが置き換えられました。 BCDEdit ツールを使用して、PFA メモリのリストの管理に関する詳細については、次を参照してください。 [PFA メモリの一覧を管理する方法](how-to-manage-the-pfa-memory-list.md)します。

 

 




