## Context-Aware Representations for Knowledge Base Relation Extraction

* ԭ�����ӣ�https://www.ukp.tu-darmstadt.de/fileadmin/user_upload/Group_UKP/publikationen/2017/2017_EMNLP_DS_relation_extraction_camera_ready.pdf*

���Ĺ�ע�������ǹ�ϵ��ȡ�еĹ�ϵ��ʾѧϰ������ȡ������Ŀ���ϵ����������ͳ�ϣ����������ֽ����������˼·��һ�������ô��Ա�ע����������ȹ��ߣ���һ��������������ģ�ͣ���CNN,Piece-wise CNN�ȡ����߽����ǰ�߶Ժ�������Ĵ���������⣬Ч�����á�����������������������Ϣ����������ϵ��ȡЧ����˼�룬���Ǿ����е������Ĺ�ϵ����Ŀ���ϵ��Ԥ��������ġ����ǣ�Ŀǰ�ķ���ֻ���Ǿ����еĵ�����ϵ��Ŀ���ϵ���������Ծ����е�������ϵ�����������⣬���������ͬʱ���Ǿ����ж����ϵ��������ģ�͡���ContextATT, ���ģ�ͻ���LSTM�������ע�������ƣ�����ͬʱѧϰ�����еĶ����ϵ��ʾ��

### ���ݼ�
���Ļ���Wikidata��Wikipedia�Ķ��빹���˵������ж����ϵ�����ݼ�������Wikipedia����link annotation��ʵ�壬����linked article��Wikidata����kbid; ����û��annotation��ʵ�壬����ʹ����Stanford CoreNLP�Ĺ��߰���������ʵ��ʶ������ʷֿ飬����Wikidata�м���kbid������ÿ��ʵ��ԣ���Wikidata�в�ѯ��ϵ�����ڼ��������ֹ�ϵ���͵�ʵ��ԣ���Ϊ�������ֱ����������200���ֶ������ľ�����ʾ������ݼ���׼ȷ�ȴﵽ79.5%��

### Relation encoder
1. token embedding: ��GloveԤѵ���Ĵ�����word embedding�Ϳ���ÿ��token��ʵ������λ��ϵ��marker embedding���,token embedding=[wordembdding ��marker embedding]
2. LSTM: ��token embedding��������ȡ��relation vector
### ContextATT 
1. �����ݼ��е�����Ķ����ϵ����ȡ��Ӧ��target relation vector ��context relation vectors
2. ���ڶ��context relation vectors, ��ע�������ƣ���������target relation vector����ضȼ���ÿ��context relation vector�ĵ÷֣����յ�context relation vector�Ƕ��context relation vectors�ļ�Ȩ��
3. ���յĹ�ϵ�����ǣ�final relation vector=[target relation vector ; context relation vector]
4. softmax

### ʵ��
���ĵ�ģ����Ŀǰstate-of-art��PCNNģ�ͣ�������LSTM��ContextSum���˶Աȣ�ʹ���˳��õ�mircro pr �� macro pr����ָ�ꡣ��baselines���, ����mirco pr��ContextATT������recall��Χ��,precision��Ч�������ã�����macro prContextATT�����еĹ�ϵ�����ж�������á�
����������ContextATT�Ȼ�����LSTM��ƽ�����������½���24%,Ч���ɹۣ���ContextSumЧ����΢���ɼ�ע�������ƺ���Ч��

### ʵ�������
���Ĺ�������ݼ��У�ÿ�����Ӷ�û�л�ֻ��һ��negative relation����͵�����һ�����⣺��ģ�͵�ʵ��Ӧ���У�����һ������s, ������ҪԤ�� <e1,?,e2>ʱ��������֪�������<e1,x,e2>��Ҳ�������ǵ���ǰ֪����Щ�й�ϵ����Щ�й�ϵ��ʵ������Ǵ�������ġ�
���������һ��������n��entity, ������ѵ��ʱ�������еļ�C(n,2)-1�������Ĺ�ϵ��������Ӧ��������C(n,2)-1����ϵ�ͺã�������Ҫ֪����Щ�й�ϵ

