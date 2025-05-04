流程图步骤序号（A:核心种子设定）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/architecture.py:Novel_architecture_generate]，{使用 core_seed_prompt 生成核心种子。该方法接收 topic, genre, number_of_chapters, word_number, user_guidance 等参数，并将它们格式化到 core_seed_prompt 提示词中。} 使用到的提示词变量名：topic, genre, number_of_chapters, word_number, user_guidance

流程图步骤序号（B:角色动力学设定）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/architecture.py:Novel_architecture_generate]，{使用 character_dynamics_prompt 生成角色动力学设定。该方法接收 core_seed, user_guidance 等参数，并将它们格式化到 character_dynamics_prompt 提示词中。} 使用到的提示词变量名：core_seed, user_guidance

流程图步骤序号（C:是否需要生成初始角色状态表）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/architecture.py:Novel_architecture_generate]，{判断 "character_dynamics_result" in partial_data and "character_state_result" not in partial_data，决定是否生成初始角色状态表。}

流程图步骤序号（D:生成初始角色状态表）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/architecture.py:Novel_architecture_generate]，{使用 create_character_state_prompt 生成初始角色状态表。该方法接收 character_dynamics 参数，并将它们格式化到 create_character_state_prompt 提示词中。} 使用到的提示词变量名：character_dynamics
- 代码2：[REPOs-AI_Novel_Generator-工程代码/architecture.py:Novel_architecture_generate]，{将生成的角色状态表保存到 character_state.txt 文件中。}

流程图步骤序号（E:世界观构建）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/architecture.py:Novel_architecture_generate]，{使用 world_building_prompt 生成世界观。该方法接收 core_seed, user_guidance 等参数，并将它们格式化到 world_building_prompt 提示词中。} 使用到的提示词变量名：core_seed, user_guidance

流程图步骤序号（F:情节架构）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/architecture.py:Novel_architecture_generate]，{使用 plot_architecture_prompt 生成情节架构。该方法接收 core_seed, character_dynamics, world_building, user_guidance 等参数，并将它们格式化到 plot_architecture_prompt 提示词中。} 使用到的提示词变量名：core_seed, character_dynamics, world_building, user_guidance

流程图步骤序号（G:章节目录生成）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/blueprint.py:Chapter_blueprint_generate]，{根据小说架构生成章节目录。该方法接收 novel_architecture, number_of_chapters, user_guidance 等参数，并根据章节数和 chunk_size 决定一次性生成还是分块生成。} 使用到的提示词变量名：novel_architecture, number_of_chapters, user_guidance (在 chapter_blueprint_prompt 中)
- 代码2：[REPOs-AI_Novel_Generator-工程代码/blueprint.py:Chapter_blueprint_generate]，{如果需要分块生成，则使用 chunked_chapter_blueprint_prompt。} 使用到的提示词变量名：novel_architecture, chapter_list, number_of_chapters, n, m, user_guidance (在 chunked_chapter_blueprint_prompt 中)

流程图步骤序号（H:是否需要分块生成章节目录）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/blueprint.py:Chapter_blueprint_generate]，{通过比较 chunk_size 和 number_of_chapters 的大小，决定是否需要分块生成章节目录。如果 chunk_size >= number_of_chapters，则一次性生成；否则，分块生成。}

流程图步骤序号（I:分块生成章节目录）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/blueprint.py:Chapter_blueprint_generate]，{当 chunk_size 小于 number_of_chapters 时，会进入分块生成章节目录的逻辑。使用 chunked_chapter_blueprint_prompt 提示词，循环生成章节目录，直到所有章节都生成完毕。} 使用到的提示词变量名：novel_architecture, chapter_list, number_of_chapters, n, m, user_guidance (在 chunked_chapter_blueprint_prompt 中)

流程图步骤序号（J:一次性生成章节目录）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/blueprint.py:Chapter_blueprint_generate]，{当 chunk_size 大于等于 number_of_chapters 时，会进入一次性生成章节目录的逻辑。使用 chapter_blueprint_prompt 提示词，一次性生成所有章节目录。} 使用到的提示词变量名：novel_architecture, number_of_chapters, user_guidance (在 chapter_blueprint_prompt 中)

流程图步骤序号（K:章节草稿生成）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/chapter.py:generate_chapter_draft]，{生成章节草稿。该方法接收各种参数，包括 api_key, base_url, model_name, filepath, novel_number, word_number, temperature, user_guidance, characters_involved, key_items, scene_location, time_constraint, embedding_api_key, embedding_url, embedding_interface_format, embedding_model_name, embedding_retrieval_k, interface_format, max_tokens, timeout。根据 novel_number 的值，选择使用 first_chapter_draft_prompt (如果 novel_number == 1) 或 next_chapter_draft_prompt (如果 novel_number > 1)。} 使用到的提示词变量名：novel_number, word_number, chapter_title, chapter_role, chapter_purpose, suspense_level, foreshadowing, plot_twist_level, chapter_summary, characters_involved, key_items, scene_location, time_constraint, user_guidance, novel_setting (在 first_chapter_draft_prompt 中) 和 user_guidance, global_summary, previous_chapter_excerpt, character_state, short_summary, novel_number, chapter_title, chapter_role, chapter_purpose, suspense_level, foreshadowing, plot_twist_level, chapter_summary, word_number, characters_involved, key_items, scene_location, time_constraint, next_chapter_number, next_chapter_title, next_chapter_role, next_chapter_purpose, next_chapter_suspense_level, next_chapter_foreshadowing, next_chapter_plot_twist_level, next_chapter_summary, filtered_context (在 next_chapter_draft_prompt 中)

流程图步骤序号（L:是否需要知识库导入）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/chapter.py:build_chapter_prompt]，{在构建章节提示词时，会调用知识库检索和处理的逻辑。通过 knowledge_search_prompt 生成检索关键词，然后从向量库中检索相关内容。}

流程图步骤序号（M:知识库导入）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/knowledge.py:import_knowledge_file]，{将知识文件导入到向量库中。该方法接收 embedding_api_key, embedding_url, embedding_interface_format, embedding_model_name, file_path, filepath 等参数。首先使用 advanced_split_content 对知识文件内容进行分段，然后加载向量库，如果向量库不存在则初始化一个新的向量库，并将分段后的内容添加到向量库中。}
- 代码2：[REPOs-AI_Novel_Generator-工程代码/chapter.py:build_chapter_prompt]，{在构建章节提示词时，会调用知识库检索和处理的逻辑。通过 knowledge_search_prompt 生成检索关键词，然后从向量库中检索相关内容。}
- 代码3：[REPOs-AI_Novel_Generator-工程代码/chapter.py:get_filtered_knowledge_context]，{对知识库内容进行过滤处理。}

流程图步骤序号（N:章节定稿）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/finalization.py:finalize_chapter]，{对指定章节进行最终处理，包括更新前文摘要、更新角色状态、插入向量库等。}


流程图步骤序号（O:是否需要扩写章节）：
- 代码1：[REPOs-AI_Novel_Generator-工程代码/finalization.py:finalize_chapter]，{在章节定稿的注释中提到，默认无需再做扩写操作，若有需要可在外部调用 enrich_chapter_text 处理后再定稿。因此，这里实际上是一个外部判断，代码本身并没有直接体现判断逻辑。}