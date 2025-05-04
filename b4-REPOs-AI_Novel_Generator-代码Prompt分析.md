# architecture.py
* [architecture.py:load_partial_architecture_data:从 filepath 下的 partial_architecture.json 读取已有的阶段性数据]
* [architecture.py:save_partial_architecture_data:将阶段性数据写入 partial_architecture.json]
* [architecture.py:Novel_architecture_generate:依次调用 core_seed_prompt, character_dynamics_prompt, world_building_prompt, plot_architecture_prompt 生成小说总体架构，并将结果输出到 Novel_architecture.txt]: core_seed_prompt, character_dynamics_prompt, world_building_prompt, plot_architecture_prompt, create_character_state_prompt

# blueprint.py
* [blueprint.py:compute_chunk_size:基于章节数和 max_tokens 计算分块大小]
* [blueprint.py:limit_chapter_blueprint:从已有章节目录中只取最近的 limit_chapters 章，以避免 prompt 超长]
* [blueprint.py:Chapter_blueprint_generate:生成章节蓝图，如果章节数 <= chunk_size，直接一次性生成，否则进行分块生成，生成完成后输出至 Novel_directory.txt]: chapter_blueprint_prompt, chunked_chapter_blueprint_prompt

# chapter.py
* [chapter.py:get_last_n_chapters_text:从目录 chapters_dir 中获取最近 n 章的文本内容，返回文本列表]
* [chapter.py:summarize_recent_chapters:根据前三章内容生成当前章节的精准摘要]: summarize_recent_chapters_prompt
* [chapter.py:extract_summary_from_response:从响应文本中提取摘要部分]
* [chapter.py:format_chapter_info:将章节信息字典格式化为文本]
* [chapter.py:parse_search_keywords:解析新版关键词格式]
* [chapter.py:apply_content_rules:应用内容处理规则]
* [chapter.py:apply_knowledge_rules:应用知识库使用规则]
* [chapter.py:get_filtered_knowledge_context:优化后的知识过滤处理]: knowledge_filter_prompt
* [chapter.py:build_chapter_prompt:构造当前章节的请求提示词]: first_chapter_draft_prompt, next_chapter_draft_prompt, knowledge_search_prompt
* [chapter.py:generate_chapter_draft:生成章节草稿，支持自定义提示词]

# common.py
* [common.py:call_with_retry:通用的重试机制封装]
* [common.py:remove_think_tags:移除 <think>...</think> 包裹的内容]
* [common.py:debug_log:打印 prompt 和 response_content]
* [common.py:invoke_with_cleaning:调用 LLM 并清理返回结果]

# finalization.py
* [finalization.py:finalize_chapter:对指定章节做最终处理：更新前文摘要、更新角色状态、插入向量库等]: summary_prompt, update_character_state_prompt

# knowledge.py
* [finalization.py:enrich_chapter_text:对章节文本进行扩写，使其更接近 word_number 字数，保持剧情连贯]
* [knowledge.py:advanced_split_content:使用基本分段策略]
* [knowledge.py:import_knowledge_file:知识文件导入至向量库]

# vectorstore_utils.py
* [vectorstore_utils.py:get_vectorstore_dir:获取 vectorstore 路径]
* [vectorstore_utils.py:clear_vector_store:清空 清空向量库]
* [vectorstore_utils.py:init_vector_store:在 filepath 下创建/加载一个 Chroma 向量库并插入 texts]
* [vectorstore_utils.py:load_vector_store:读取已存在的 Chroma 向量库。若不存在则返回 None]
* [vectorstore_utils.py:split_by_length:按照 max_length 切分文本]
* [vectorstore_utils.py:split_text_for_vectorstore:对新的章节文本进行分段后,再用于存入向量库]
* [vectorstore_utils.py:update_vector_store:将最新章节文本插入到向量库中]
* [vectorstore_utils.py:get_relevant_context_from_vector_store:从向量库中检索与 query 最相关的 k 条文本，拼接后返回]
* [vectorstore_utils.py:_get_sentence_transformer:获取sentence transformer模型，处理SSL问题]