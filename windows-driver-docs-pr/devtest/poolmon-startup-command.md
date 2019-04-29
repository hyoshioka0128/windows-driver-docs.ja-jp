---
title: PoolMon のスタートアップ コマンド
description: PoolMon を起動するには、次の構文とパラメーターを使用してコマンドラインでコマンドを入力します。
ms.assetid: 2aa0cf09-f016-46b9-af4e-0f3fbc6fbe5b
keywords:
- PoolMon スタートアップ コマンドのドライバーの開発ツール
topic_type:
- apiref
api_name:
- PoolMon Startup Command
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c54fc24ff48c57464085a048da380b8a2afdb7f8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327114"
---
# <a name="poolmon-startup-command"></a>PoolMon のスタートアップ コマンド


PoolMon を起動するには、次の構文とパラメーターを使用してコマンドラインでコマンドを入力します。

```
    poolmon [/iTag] [/xTag] [/c [LocalTagFile]] [/g [PoolTagFile]] [/s[TSSessionID]] [ /p | /p /p ] [/e] [/( | /)]  [/t | /a| /f| /d | /b| /m] [/l] [/n [File]] [/? | /h] 
```

## <a name="span-idddkpoolmonstartupcommandtoolsspanspan-idddkpoolmonstartupcommandtoolsspanparameters"></a><span id="ddk_poolmon_startup_command_tools"></span><span id="DDK_POOLMON_STARTUP_COMMAND_TOOLS"></span>パラメーター


<span id="________i______"></span><span id="________I______"></span> **/i**   
指定されたプール タグを持つ割り当てのみが表示されます。 複数 **/i** PoolMon コマンドのパラメーター。 間にスペースを入力しないでください、 **/i**と*タグ*引数。

<span id="________x______"></span><span id="________X______"></span> **/x**   
表示からタグを指定して割り当てを除外します。 複数 **/x** PoolMon コマンドのパラメーター。 間にスペースを入力しないでください、 **/x**と*タグ*引数。

<span id="_______Tag______"></span><span id="_______tag______"></span><span id="_______TAG______"></span> *タグ*   
プール タグまたはプール タグのパターンを指定します。 プール タグは、大文字小文字が区別されます。 *タグ*引数は、アスタリスクを含めることができます (**\\* * *) を任意の文字または疑問符 () の 0 個以上のインスタンスを表す (*<em>?</em>*) を任意の文字の 1 つのインスタンスを表します。 アスタリスクを持つタグは開始されません。

<span id="________c______"></span><span id="________C______"></span> **/c**   
表示する列を追加します (マップ済み\_ドライバー) 各プール タグを使用するローカル コンピューターのドライバーの一覧を表示します。 この機能は、32 ビット バージョンの Windows でのみサポートされます。

<span id="_______LocalTagFile______"></span><span id="_______localtagfile______"></span><span id="_______LOCALTAGFILE______"></span> *LocalTagFile*   
タグのローカル ファイルや、ローカル コンピューター上のドライバーの一覧を含む書式設定されたテキスト ファイルを割り当てることがタグの値のパスとファイル名を指定します。 このファイルは、マップ先のデータ ソース\_ドライバー列を使用するときに表示される、 **/c**パラメーター。 既定では localtag.txt です。

使用する場合、 **/c**パラメーターの値を指定しないで*LocalTagFile*PoolMon では、現在のディレクトリには、localtag.txt ファイルが見つからない、PoolMon をスキャンして localtag.txt ファイルを生成すると、ローカル コンピューター上のドライバー (%systemroot%\\System32\\ドライバー\\\*.sys)。

<span id="________g______"></span><span id="________G______"></span> **/g**   
表示する列を追加します (マップ済み\_ドライバー) Windows のコンポーネントと各タグを割り当てることがよく使用されるドライバーの一覧を表示します。

<span id="_______PoolTagFile______"></span><span id="_______pooltagfile______"></span><span id="_______POOLTAGFILE______"></span> *PoolTagFile*   
Windows コンポーネントの名前を示し、ドライバーおよびタグの値を割り当てることが一般的に使用する書式設定されたテキスト ファイルのパスとファイル名を指定します。 このファイルは、マップ先のデータ ソース\_ドライバー列を使用するときに表示される、 **/g**パラメーター。

既定では pooltag.txt、Microsoft によって提供されるファイルです。 *Pooltag.txt* 、ツールに含まれる\\Windows Driver Kit (WDK) の他のサブディレクトリ。

<span id="________s______"></span><span id="________S______"></span> **/s**   
ターミナル サービス セッションのプールから割り当てを表示します。

<span id="_______TSSessionID______"></span><span id="_______tssessionid______"></span><span id="_______TSSESSIONID______"></span> *TSSessionID*   
指定したセッションのプールから割り当てのみが表示されます。 間にスペースを入力しないでください、 **/s**パラメーターおよび*TSSessionID*引数。

<span id="________p______"></span><span id="________P______"></span> **/p**   
非ページ プールから割り当てのみが表示されます。

<span id="________p__p_______"></span><span id="________P__P_______"></span> **/p/p**   
ページ プールから割り当てのみが表示されます。

<span id="________e_______"></span><span id="________E_______"></span> **/e**   
プールの合計が表示されます。 ディスプレイ画面の下部にある、合計が表示されます。

<span id="__________or___"></span><span id="__________OR___"></span> **/(** または **/)**  
並べ替えの変更でモードをオンにします。 **/(** または **/)** 値の代わりに (割り当て、無料の操作とバイト) の値で PoolMon を並べ替えます。 各値の変更は、値の後に、かっこ内に表示されます。

使用して **/a**、 **/f**、 **/b**または **/m**します。 たとえば、 **poolmon/a**割り当て数で表示を並べ替えます中**poolmon/(/a**割り当ての数を変更して、表示を並べ替えます。

左かっこと右かっこ文字効果は同じと同じ意味で使用できます。

<span id="________t______"></span><span id="________T______"></span> **/t**   
タグ名でアルファベット順に並べ替えを行います。 これが既定値です。

<span id="________a______"></span><span id="________A______"></span> **/a**   
タグの割り当ての数によって並べ替えます。

<span id="________f_______"></span><span id="________F_______"></span> **/f**   
タグは、無料の操作の数によって並べ替えます。

<span id="________d______"></span><span id="________D______"></span> **/d**   
タグは、バイトの割り当てと解放されるバイトの違いによって並べ替えます。

<span id="________b_______"></span><span id="________B_______"></span> **/b**   
タグを使用されているバイト順に並べ替えます。

<span id="________m_______"></span><span id="________M_______"></span> **/m**   
タグを割り当てるあたりのバイトの順に並べ替えます。

<span id="________l______"></span><span id="________L______"></span> **/l**   
オフの強調表示をオンにします。 既定では、PoolMon には、最後の更新以降に変更された値が強調表示されます。

<span id="________n______"></span><span id="________N______"></span> **/n**   
コマンド ウィンドウに表示する代わりに、ファイルを PoolMon 出力のスナップショットを保存します。 出力を構成するその他のコマンド ライン パラメーターを含めることができます。

スナップショット データは静的であるために、PoolMon 表示内の値に変更を表示する列は、スナップショット ファイルには表示されません。

<span id="_______File______"></span><span id="_______file______"></span><span id="_______FILE______"></span> *ファイル*   
スナップショット ファイルの場所と名前を指定します。 既定では poolsnap.log です。

<span id="__________or__h"></span><span id="__________OR__H"></span> **/?** または **/h**  
コマンドライン構文を表示します。 **/でしょうか。** **/h**パラメーターの効果は同じと同じ意味で使用できます。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

PoolMon には、Windows Server 2003 の 64 ビット版で localtag.txt ファイルを生成できません。 結果として、 **/c**パラメーターとその機能は Windows の 32 ビット バージョンでのみ使用できます。

使用することができます、 **/c**と **/g**同じコマンド内のパラメーター。 その場合、マップされた\_ドライバー列には、ローカルのタグとタグ ファイルをプールからのデータが表示されます。

使用することも **/c**と **/g** 、マップ先の他のファイルからデータを表示する\_ドライバー ファイルを指定する列の名前と場所のいずれかのパラメーター **poolmon/c***filename*または**poolcom/g** *filename*します。 ここで、 **/c**と **/g**パラメーターの動作は同じと同じ意味で使用できます。

ターミナル サービス セッション プールの監視は、Windows Server 2003 および Windows の以降のバージョンでのみ使用できます。

Win32 サブシステムのカーネル モードの部分は、コンピューターがターミナル サーバーとして構成されている場合にのみ、ターミナル サービス セッションのプールからメモリを割り当てます。 それ以外の場合、Windows は、システムのプールからターミナル サービスのプールのメモリを割り当てます。









