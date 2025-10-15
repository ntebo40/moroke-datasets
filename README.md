# moroke-datasets
datasets/ notebooks/ models/ supplementary/ README.md
# ============================================================================
# FIGURE 6: COMPREHENSIVE METHODOLOGY BLUEPRINT
# ============================================================================

def create_comprehensive_methodology_blueprint():
    """Create detailed visual blueprint of the hybrid framework"""
    
    fig = plt.figure(figsize=(20, 24))
    ax = plt.axes([0, 0, 1, 1])
    ax.set_xlim(0, 10)
    ax.set_ylim(0, 30)
    ax.axis('off')
    
    # Color scheme
    colors = {
        'phase': '#2E86AB',
        'theory': '#F18F01', 
        'computation': '#06A77D',
        'validation': '#E63946',
        'application': '#9D4EDD',
        'output': '#FFB703'
    }
    
    # Helper functions
    def draw_box(x, y, width, height, text, color, alpha=0.8, fontsize=10):
        """Draw a rounded rectangle box"""
        from matplotlib.patches import FancyBboxPatch
        box = FancyBboxPatch((x, y), width, height,
                            boxstyle="round,pad=0.1",
                            facecolor=color, edgecolor='black',
                            linewidth=2.5, alpha=alpha)
        ax.add_patch(box)
        
        # Wrap text
        wrapped = '\n'.join([text[i:i+20] for i in range(0, len(text), 20)])
        ax.text(x + width/2, y + height/2, wrapped,
               ha='center', va='center', fontsize=fontsize,
               fontweight='bold', color='white' if alpha > 0.7 else 'black')
    
    def draw_arrow(x1, y1, x2, y2, style='->', color='black', width=2.5):
        """Draw arrow between boxes"""
        ax.annotate('', xy=(x2, y2), xytext=(x1, y1),
                   arrowprops=dict(arrowstyle=style, lw=width, 
                                 color=color, alpha=0.8))
    
    def draw_diamond(x, y, size, text, color):
        """Draw decision diamond"""
        from matplotlib.patches import FancyBboxPatch
        diamond = FancyBboxPatch((x-size/2, y-size/2), size, size,
                                boxstyle="round,pad=0.05",
                                facecolor=color, edgecolor='black',
                                linewidth=2.5, alpha=0.8,
                                transform=ax.transData)
        # Rotate to make diamond
        import matplotlib.transforms as transforms
        t = transforms.Affine2D().rotate_deg(45) + ax.transData
        diamond.set_transform(t)
        ax.add_patch(diamond)
        ax.text(x, y, text, ha='center', va='center',
               fontsize=9, fontweight='bold', color='white')
    
    # ========================================================================
    # TITLE
    # ========================================================================
    ax.text(5, 29, 'HYBRID BSEM-NEURAL FRAMEWORK',
           ha='center', fontsize=20, fontweight='bold',
           bbox=dict(boxstyle='round', facecolor='lightblue', 
                    edgecolor='navy', linewidth=3, alpha=0.9))
    ax.text(5, 28.3, 'Methodological Blueprint for Organizational Research',
           ha='center', fontsize=14, style='italic')
    
    # ========================================================================
    # PHASE 1: THEORETICAL FOUNDATION (Top)
    # ========================================================================
    draw_box(0.2, 26, 9.6, 1.2, 'PHASE 1: THEORETICAL FOUNDATION',
            colors['phase'], fontsize=13)
    
    # Theory boxes
    draw_box(0.5, 23.5, 2, 1.8, 
            'Theory Selection\n\n• COR Theory\n• Justice Theory\n• Integration',
            colors['theory'], alpha=0.7, fontsize=9)
    
    draw_box(3, 23.5, 2, 1.8,
            'Construct\nOperationalization\n\n• Bullying\n• Depletion\n• Justice',
            colors['theory'], alpha=0.7, fontsize=9)
    
    draw_box(5.5, 23.5, 2, 1.8,
            'Structural Paths\n\n• H1-H4\n• Meta-analytic\n• Calibration',
            colors['theory'], alpha=0.7, fontsize=9)
    
    draw_box(8, 23.5, 1.5, 1.8,
            'Expected\nNonlinearity\n\n• Thresholds\n• Buffering',
            colors['theory'], alpha=0.7, fontsize=9)
    
    # Arrows from phase to components
    draw_arrow(5, 26, 1.5, 25.3)
    draw_arrow(5, 26, 4, 25.3)
    draw_arrow(5, 26, 6.5, 25.3)
    draw_arrow(5, 26, 8.75, 25.3)
    
    # ========================================================================
    # PHASE 2: COMPUTATIONAL ARCHITECTURE
    # ========================================================================
    draw_box(0.2, 21, 9.6, 1.2, 'PHASE 2: COMPUTATIONAL ARCHITECTURE',
            colors['computation'], fontsize=13)
    
    # Bayesian SEM Component
    draw_box(0.5, 17.5, 3, 2.8,
            'BAYESIAN SEM\n\n• Measurement Model\n  λ, τ, θ²\n\n• Structural Model\n  β, ψ²\n\n• Prior Specification\n  Weakly Informative',
            colors['computation'], alpha=0.7, fontsize=9)
    
    # Neural Encoder Component  
    draw_box(4, 17.5, 3, 2.8,
            'NEURAL ENCODER\n\n• Architecture: 8-8-1\n• Activation: ReLU\n• Regularization: L2\n\n• Captures:\n  Thresholds,\n  Interactions,\n  Nonlinearities',
            colors['computation'], alpha=0.7, fontsize=9)
    
    # Integration Component
    draw_box(7.5, 17.5, 2, 2.8,
            'HYBRID\nINTEGRATION\n\n• BSEM → η\n• η → Neural\n• Uncertainty\n  Propagation',
            colors['computation'], alpha=0.7, fontsize=9)
    
    # Arrows from theory to computation
    draw_arrow(1.5, 23.5, 2, 20.3)
    draw_arrow(4, 23.5, 5.5, 20.3)
    draw_arrow(6.5, 23.5, 5.5, 20.3)
    draw_arrow(8.75, 23.5, 8.5, 20.3)
    
    # Arrows within computation phase
    draw_arrow(3.5, 19, 4, 19)
    draw_arrow(7, 19, 7.5, 19)
    
    # ========================================================================
    # MCMC ESTIMATION
    # ========================================================================
    draw_box(1.5, 15.5, 7, 1.2,
            'MCMC ESTIMATION: NUTS Sampler | 4 Chains × 5000 Iterations',
            '#6C757D', fontsize=11)
    
    draw_arrow(2, 17.5, 3, 16.7)
    draw_arrow(5.5, 17.5, 5, 16.7)
    draw_arrow(8.5, 17.5, 7, 16.7)
    
    # ========================================================================
    # PHASE 3: VALIDATION & DIAGNOSTICS
    # ========================================================================
    draw_box(0.2, 13.5, 9.6, 1.2, 'PHASE 3: VALIDATION & DIAGNOSTICS',
            colors['validation'], fontsize=13)
    
    # Convergence Diagnostics
    draw_box(0.5, 10.5, 2.2, 2.3,
            'Convergence\nDiagnostics\n\n✓ R̂ = 1.00\n✓ ESS > 2000\n✓ MCSE < 0.003\n✓ Traceplots',
            colors['validation'], alpha=0.7, fontsize=8)
    
    # Parameter Recovery
    draw_box(3, 10.5, 2.2, 2.3,
            'Parameter\nRecovery\n\n✓ Bias < 0.10\n✓ Coverage 100%\n✓ RMSE low\n✓ All H1-H4',
            colors['validation'], alpha=0.7, fontsize=8)
    
    # Model Fit
    draw_box(5.5, 10.5, 1.8, 2.3,
            'Model Fit\n\n✓ WAIC\n✓ LOO\n✓ Bayes R²\n✓ PPCs',
            colors['validation'], alpha=0.7, fontsize=8)
    
    # Benchmarking
    draw_box(7.5, 10.5, 2, 2.3,
            'Benchmarking\n\n• vs. 6 Models\n• RMSE, R²\n• CRPS\n• Composite',
            colors['validation'], alpha=0.7, fontsize=8)
    
    # Arrows to validation
    draw_arrow(5, 15.5, 1.6, 12.8)
    draw_arrow(5, 15.5, 4.1, 12.8)
    draw_arrow(5, 15.5, 6.4, 12.8)
    draw_arrow(5, 15.5, 8.5, 12.8)
    
    # ========================================================================
    # DECISION GATE
    # ========================================================================
    draw_diamond(5, 8.5, 1.8, 'ALL\nCHECKS\nPASS?', '#FFD700')
    
    draw_arrow(1.6, 10.5, 4.5, 9)
    draw_arrow(4.1, 10.5, 4.8, 9)
    draw_arrow(6.4, 10.5, 5.2, 9)
    draw_arrow(8.5, 10.5, 5.5, 9)
    
    # NO path (revision loop)
    draw_arrow(4.2, 8.5, 1.5, 17, color='red', width=2)
    ax.text(2.5, 12, 'NO\nRevise Model', fontsize=10, color='red',
           fontweight='bold', ha='center',
           bbox=dict(boxstyle='round', facecolor='mistyrose', 
                    edgecolor='red', linewidth=2))
    
    # YES path
    draw_arrow(5, 7.7, 5, 6.8, color='green', width=3)
    ax.text(5.5, 7.2, 'YES', fontsize=11, color='green', fontweight='bold')
    
    # ========================================================================
    # PHASE 4: APPLICATION & INTERPRETATION
    # ========================================================================
    draw_box(0.2, 5.5, 9.6, 1.2, 'PHASE 4: EMPIRICAL APPLICATION',
            colors['application'], fontsize=13)
    
    # Ethical Implementation
    draw_box(0.5, 2.8, 2.2, 2,
            'Ethical\nImplementation\n\n• IRB Approval\n• Informed Consent\n• Privacy\n• Intervention',
            colors['application'], alpha=0.7, fontsize=9)
    
    # Output Interpretation
    draw_box(3, 2.8, 2.2, 2,
            'Result\nInterpretation\n\n• β paths\n• Neural patterns\n• Theory validation\n• Recommendations',
            colors['application'], alpha=0.7, fontsize=9)
    
    # Reproducibility
    draw_box(5.5, 2.8, 2.2, 2,
            'Reproducibility\n\n• Code archive\n• Synthetic data\n• Documentation\n• OSF deposit',
            colors['application'], alpha=0.7, fontsize=9)
    
    # Dissemination
    draw_box(8, 2.8, 1.5, 2,
            'Dissemination\n\n• Publication\n• Policy brief\n• Training',
            colors['application'], alpha=0.7, fontsize=9)
    
    # Arrows to application
    draw_arrow(5, 5.5, 1.6, 4.8)
    draw_arrow(5, 5.5, 4.1, 4.8)
    draw_arrow(5, 5.5, 6.6, 4.8)
    draw_arrow(5, 5.5, 8.75, 4.8)
    
    # ========================================================================
    # FINAL OUTPUTS
    # ========================================================================
    draw_box(1, 0.8, 8, 1.5,
            'VALIDATED FRAMEWORK FOR ORGANIZATIONAL RESEARCH\n\n' +
            '✓ High Predictive Accuracy (R² = 0.293)  |  ' +
            '✓ Theoretical Interpretability (All H1-H4)  |  ' +
            '✓ Nonlinear Flexibility',
            colors['output'], fontsize=11)
    
    draw_arrow(1.6, 2.8, 3, 2.3)
    draw_arrow(4.1, 2.8, 4.5, 2.3)
    draw_arrow(6.6, 2.8, 6, 2.3)
    draw_arrow(8.75, 2.8, 7, 2.3)
    
    # ========================================================================
    # SIDE ANNOTATIONS
    # ========================================================================
    
    # Key metrics box
    metrics_text = """
    KEY PERFORMANCE METRICS
    ━━━━━━━━━━━━━━━━━━━━━━━━
    
    Convergence:
    • R̂ = 1.00 (all parameters)
    • ESS = 2,585 (mean)
    • MCSE < 0.003
    
    Recovery:
    • Mean |Bias| = 0.064
    • Coverage = 100%
    
    Fit:
    • Bayesian R² = 0.499
    • WAIC = 1051.06
    • All PPPs ∈ [0.05, 0.95]
    
    Benchmark:
    • 192.5% vs Linear
    • 63.1% vs Standard SEM
    • 52.6% vs Bayesian SEM
    
    Composite Score: 2.037
    (28% better than next best)
    """
    
    ax.text(10.2, 20, metrics_text, fontsize=8, family='monospace',
           verticalalignment='top',
           bbox=dict(boxstyle='round', facecolor='lightyellow',
                    edgecolor='orange', linewidth=2, alpha=0.9))
    
    # Legend
    legend_elements = [
        ('Theoretical', colors['theory']),
        ('Computational', colors['computation']),
        ('Validation', colors['validation']),
        ('Application', colors['application'])
    ]
    
    for i, (label, color) in enumerate(legend_elements):
        y_pos = 15 - i*0.8
        ax.add_patch(plt.Rectangle((10.2, y_pos), 0.3, 0.5,
                                   facecolor=color, edgecolor='black',
                                   linewidth=1, alpha=0.7))
        ax.text(10.6, y_pos+0.25, label, fontsize=9, va='center')
    
    # Software stack
    software_text = """
    SOFTWARE STACK
    ━━━━━━━━━━━━━━━━
    
    • R: blavaan, lavaan
    • Python: PyMC3, PyTorch
    • Diagnostics: ArviZ
    • Viz: Matplotlib, Seaborn
    """
    
    ax.text(10.2, 12, software_text, fontsize=8, family='monospace',
           verticalalignment='top',
           bbox=dict(boxstyle='round', facecolor='lightcyan',
                    edgecolor='blue', linewidth=2, alpha=0.9))
    
    # Citation
    ax.text(5, 0.2, 
           'Moroke, N.D. (2025). Resolving the Methodological Trilemma: ' +
           'A Hybrid Bayesian SEM-Neural Framework',
           ha='center', fontsize=8, style='italic')
    
    plt.tight_layout()
    plt.savefig('/mnt/user-data/outputs/Figure_6_Methodology_Blueprint.png',
                dpi=300, bbox_inches='tight', facecolor='white')
    plt.show()
    
    print("\n✅ Figure 6: Comprehensive Methodology Blueprint completed!")

# Execute
create_comprehensive_methodology_blueprint()
