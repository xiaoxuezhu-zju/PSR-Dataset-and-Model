# psr-dataset
# Enhancing Neural Theorem Proving via High-Quality Data Selection and Verifier Feedback

This repository accompanies our work on data-centric neural theorem proving for Isabelle/HOL. We study how to improve proof generation by selecting higher-quality formal proof data and by using Isabelle verifier feedback during inference.

Our framework has two main components:

- **PSR-guided high-quality data selection**: we select Isabelle theorem-proof pairs according to proof complexity, semantic coverage, and reasoning diversity.
- **Dynamic feedback-based prompt optimization**: we use Isabelle verifier feedback from failed proof attempts to guide later generations.

Using only a compact PSR-selected training set, our LoRA fine-tuned model achieves strong performance on the Isabelle portion of miniF2F. When combined with verifier-feedback-guided inference, the full framework reaches **90.6% Pass@64** on miniF2F-test.

## Released Resources

We release both the selected dataset and the LoRA adapter fine-tuned from DeepSeek-Math-7B-Base.

| Resource | Description | Link |
| --- | --- | --- |
| Dataset | PSR-selected Isabelle/HOL theorem-proof dataset with 4,271 examples | [Hugging Face Dataset](https://huggingface.co/datasets/xiaoxuezhu/PSR_Selected_Isabelle_Proof_Dataset) |
| Model | LoRA adapter fine-tuned from DeepSeek-Math-7B-Base for Isabelle proof generation | [Hugging Face Model](https://huggingface.co/xiaoxuezhu/deepseek-math-isabelle-prover-lora) |

## Dataset

The released dataset is selected from a larger Isabelle/HOL and Archive of Formal Proofs (AFP) corpus. The selection process follows the PSR criterion:

- **Proof Complexity**: keeps examples with useful reasoning structure and moderate difficulty.
- **Semantic Coverage**: encourages broad coverage across theorem domains and problem types.
- **Reasoning Diversity**: promotes diverse Isabelle tactics and proof strategies.

The final dataset contains **4,271 theorem-proof pairs** and is designed for supervised fine-tuning of proof-generation models.

## Results

We evaluate on the Isabelle portion of miniF2F using Isabelle 2025 and the PISA environment.

| Method | Training Data | Sample Budget | miniF2F-test |
| --- | ---: | ---: | ---: |
| No fine-tuning | - | 64 attempts | 42.6% |
| Raw corpus SFT | ~200,000 examples | 64 attempts | 53.7% |
| High-quality data SFT | ~4,200 examples | 64 attempts | 84.8% |
| Full framework with verifier feedback | ~4,200 examples | 64 attempts | 90.6% |

## Citation

If you use our dataset, model, or code, please cite:

```bibtex
@inproceedings{zhu2026enhancing,
  title={Enhancing Neural Theorem Proving via High-Quality Data Selection and Verifier Feedback},
  author={Zhu, Xiaoxue and Hu, Jilin and Zhang, Fuyuan and Zhang, Jianyu and Zhao, Yongwang},
  booktitle={Proceedings of the 43rd International Conference on Machine Learning},
  year={2026}
}
```

## License

Please refer to the licenses and terms of the released Hugging Face dataset, the LoRA adapter, the DeepSeek-Math-7B-Base model, Isabelle/HOL, and AFP. Generated proofs should always be independently checked by Isabelle before use.
